<script lang="ts">
  import AppBar from "./AppBar.svelte"

  let isOpen : boolean = false
  let isSent : boolean = false
  let fromMain : string = undefined

  const sendMessageToElectron = () => {
    if (window.Main) {
      window.Main.sendMessage("Hello I'm from React World");
    } else {
      fromMain = "You are in a Browser, so no Electron functions are available";
    }
    isSent = true
  };

  const handleToggle = () => {
    console.log("Test")
    if (isOpen) {
      isOpen = false
      isSent = false
    } else {
      isOpen = true
      fromMain = null
    }
  };

  if (window.Main) {
    window.Main.on("message", (message: string) => {
      fromMain = message
    });
  }
  
</script>

<div class="flex flex-col h-screen">
  {#if window.Main}
    <div class="flex-none">
      <AppBar />
    </div>
  {/if}
  <div class="flex-auto">
    <div
      class=" flex flex-col justify-center items-center h-full bg-gray-800 space-y-4"
    >
      <h1 class="text-2xl text-gray-200">
        Vite + Svelte2 + Typescript + Electron + Tailwind
      </h1>
      <button
        class="bg-yellow-400 py-2 px-4 rounded focus:outline-none shadow hover:bg-yellow-200"
        on:click={() => handleToggle()}
      >
        Click Me
      </button>
      {#if isOpen}
        <div class="flex flex-col space-y-4 items-center">
          <div class="flex space-x-3">
            <h1 class="text-xl text-gray-50">
              💝 Welcome 💝, now send a message to the Main 📩📩
            </h1>
            <button
              on:click={() => sendMessageToElectron()}
              class="bg-green-400 rounded px-4 py-0 focus:outline-none hover:bg-green-300"
            >
              Send
            </button>
          </div>
          {#if isSent}
            <div>
              <h4 class="text-green-500">Message sent!!</h4>
            </div>
          {/if}
          {#if fromMain}
            <div>
              <h4 class=" text-yellow-200">{fromMain}</h4>
            </div>
          {/if}
        </div>
      {/if}
    </div>
  </div>
</div>
