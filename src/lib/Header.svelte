<script lang="ts">
    import {
      ListBox,
      ListBoxItem,
      popup,
      type PopupSettings,
    } from "@skeletonlabs/skeleton";
    import dayjs from "dayjs";
    import "dayjs/locale/ar";
  
    // Set locale globally
    dayjs.locale("ar");
  
    // Determine morning/evening
    let prd = dayjs().format("a") === "م" ? "مساء" : "صباح";
  
    // State for combobox selection
    let comboboxValue: string = "📚 جميع المهام";
  
    $: console.log("Selected:", comboboxValue);
  
    // Popup settings for the dropdown
    const popupCombobox: PopupSettings = {
      event: "click",
      target: "popupCombobox",
      placement: "bottom",
      closeQuery: ".listbox-item",
    };
  </script>
  
  <header class="flex justify-between">
    <div>
      <h1 class="text-4xl mb-2">{prd} الخير 👋</h1>
      <h2 class="text-2xl text-surface-900/50">
        {dayjs().format("dddd D MMMM YYYY")}
      </h2>
    </div>
  
    <!-- Button to trigger the popup -->
    <button
      class="btn variant-filled w-48 h-fit py-4 justify-between"
      use:popup={popupCombobox}
    >
      <span class="capitalize">{comboboxValue || "حدد خيارًا"}</span>
      <span>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="36"
          viewBox="0 0 24 24"
        >
          <path
            fill="currentColor"
            d="m13 16.172l5.364-5.364l1.414 1.414L12 20l-7.778-7.778l1.414-1.414L11 16.172V4h2z"
          />
        </svg>
      </span>
    </button>
  
    <!-- Popup dropdown -->
    <div class="card w-48 shadow-xl py-2" data-popup="popupCombobox">
      <ListBox bind:value={comboboxValue} rounded="rounded-none">
        <ListBoxItem bind:group={comboboxValue} name="task" value="📚 جميع المهام">
          📚 جميع المهام
        </ListBoxItem>
        <ListBoxItem bind:group={comboboxValue} name="task" value="🎬 مهام اليوم">
          🎬 مهام اليوم
        </ListBoxItem>
      </ListBox>
      <div class="arrow bg-surface-100-800-token" />
    </div>
  </header>
  