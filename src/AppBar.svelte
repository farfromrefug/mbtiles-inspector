<script lang="ts">
  import Icon from "./assets/icons/Icon-Electron.png";
  let isMaximize = false;

  const handleToggle = () => {
    isMaximize = !isMaximize;
    window.Main.Maximize();
  };
</script>

<div class="py-0.5 flex justify-between draggable">
  <div class="inline-flex">
    <img class="h-6 lg:-ml-2" src={Icon} alt="Icon of Electron" />
    <p class="text-xs md:pt-1 md:-ml-1 lg:-ml-2">Vite App</p>
  </div>
  <div class="inline-flex -mt-1">
    <button
      on:click={() => window.Main.Minimize()}
      class="undraggable md:px-4 lg:px-3 pt-1 hover:bg-gray-300"
    >
      &#8211;
    </button>
    <button
      on:click={() => handleToggle()}
      class="undraggable px-6 lg:px-5 pt-1 hover:bg-gray-300"
    >
      {isMaximize ? "\u2752" : "⃞"}
    </button>
    <button
      on:click={() => window.Main.Close()}
      class="undraggable px-4 pt-1 hover:bg-red-500 hover:text-white"
    >
      &#10005;
    </button>
  </div>
</div>
<div class="bg-gray-900 text-white undraggable">
  <div class="flex text-center">
    <div class="text-sm w-8  hover:bg-gray-700">File</div>
    <div class="text-sm w-8   hover:bg-gray-700">Edit</div>
    <div class="text-sm w-10  hover:bg-gray-700">View</div>
    <div class="text-sm w-14  hover:bg-gray-700 ">Window</div>
    <div class="text-sm w-9  hover:bg-gray-700 ">Help</div>
  </div>
</div>

<style>
  .draggable {
    -webkit-user-select: none;
    -webkit-app-region: drag;
  }

  .draggable button {
    -webkit-app-region: no-drag;
  }
</style>
