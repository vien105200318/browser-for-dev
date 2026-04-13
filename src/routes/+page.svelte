<script lang="ts">
  import { Webview } from '@tauri-apps/api/webview';
  import { getCurrentWindow } from '@tauri-apps/api/window';

  let url = "https://google.com";
  let isLoading = false;
  let errorMessage = "";

  let mobileContainer: HTMLDivElement;
  let desktopContainer: HTMLDivElement;

  let mobileWebview: Webview | null = null;
  let desktopWebview: Webview | null = null;

  async function loadWeb() {
    if (!url.startsWith("http")) url = "https://" + url;
    isLoading = true;
    errorMessage = "";

    const appWindow = getCurrentWindow();

    // Dọn dẹp cửa sổ cũ (Bọc try-catch chống crash)
    if (mobileWebview) {
      try { await mobileWebview.close(); } catch (e) { console.log("Mobile cũ đã bay màu."); }
    }
    if (desktopWebview) {
      try { await desktopWebview.close(); } catch (e) { console.log("Desktop cũ đã bay màu."); }
    }

    try {
      const mRect = mobileContainer.getBoundingClientRect();
      const dRect = desktopContainer.getBoundingClientRect();

      // Dùng Date.now() để tên window luôn là duy nhất
      const timeId = Date.now();
      const mLabel = `mobile-${timeId}`;
      const dLabel = `desktop-${timeId}`;

      // Triệu hồi Native Webview Cửa sổ con
      mobileWebview = new Webview(appWindow, mLabel, {
        url: url,
        x: Math.round(mRect.left),
        y: Math.round(mRect.top),
        width: Math.round(mRect.width),
        height: Math.round(mRect.height)
      });

      desktopWebview = new Webview(appWindow, dLabel, {
        url: url,
        x: Math.round(dRect.left),
        y: Math.round(dRect.top),
        width: Math.round(dRect.width),
        height: Math.round(dRect.height)
      });

    } catch (error) {
      console.error(error);
      errorMessage = String(error);
    }
    
    isLoading = false;
  }
</script>

<main class="h-screen w-screen flex flex-col bg-gray-900 text-white overflow-hidden relative">
  <div class="h-14 bg-gray-800 flex items-center px-4 gap-4 border-b border-gray-700 shadow-md z-10 relative">
    <div class="font-bold text-xl bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">
      DevBrowse
    </div>
    
    <div class="flex-1 flex max-w-3xl relative">
      <input 
        type="text" 
        bind:value={url} 
        on:keydown={(e) => e.key === 'Enter' && loadWeb()}
        class="w-full bg-gray-900 border border-gray-600 px-4 py-1.5 rounded-md text-sm outline-none focus:border-blue-500 transition"
        placeholder="Nhập URL (VD: google.com) và ấn Enter..."
      />
    </div>

    <button 
      on:click={loadWeb} 
      disabled={isLoading}
      class="bg-blue-600 hover:bg-blue-500 disabled:bg-gray-600 px-6 py-1.5 rounded-md font-medium transition"
    >
      {isLoading ? "Đang xử lý..." : "Duyệt"}
    </button>
  </div>

  {#if errorMessage}
    <div class="bg-red-500 text-white px-4 py-2 text-center text-sm z-20 relative">
      LỖI: {errorMessage}
    </div>
  {/if}

  <div class="flex-1 p-6 flex gap-8 overflow-auto bg-gray-950 items-start justify-center relative">
    
    <div class="flex flex-col items-center gap-3 shrink-0">
      <div class="flex items-center gap-2">
        <span class="text-sm font-semibold text-gray-300">iPhone 14 Pro</span>
      </div>
      <div 
        bind:this={mobileContainer}
        class="w-[393px] h-[852px] bg-transparent rounded-3xl border-[12px] border-gray-800 shadow-2xl relative overflow-hidden"
      >
        <div class="absolute inset-0 flex items-center justify-center text-gray-600 text-center px-4 -z-10">
          Đang tải Webview...
        </div>
      </div>
    </div>

    <div class="flex flex-col items-center gap-3 shrink-0">
      <div class="flex items-center gap-2">
        <span class="text-sm font-semibold text-gray-300">iPad Mini</span>
      </div>
      <div 
        bind:this={desktopContainer}
        class="w-[768px] h-[1024px] bg-transparent rounded-2xl border-[12px] border-gray-800 shadow-2xl relative overflow-hidden"
      >
        <div class="absolute inset-0 flex items-center justify-center text-gray-600 text-center px-4 -z-10">
          Đang tải Webview...
        </div>
      </div>
    </div>

  </div>
</main>