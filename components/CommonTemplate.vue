<template name="common-slide">
  <div>
    <slot></slot>
    <div class="pt-12">
      <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
        Press Space for next page <carbon:arrow-right class="inline"/>
      </span>
    </div>
    <div class="abs-br m-6 flex gap-2">
      <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
        <carbon:edit />
      </button>
    </div>
  </div>
</template>
<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>
