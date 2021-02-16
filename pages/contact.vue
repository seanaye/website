<template>
  <div class="mt-12 py-12 px-6 mb-4 md:p-20 leading-relaxed">
    <h1 class="text-4xl font-semibold">Contact</h1>
    <p class="text-xl leading-relaxed">Let's chat over tea or a cocktail.</p>

    <!-- new person -->
    <div class="max-w-sm bg-white shadow-lg rounded-lg overflow-hidden my-4">
      <div class="py-4 px-6">
        <p class="py-2 text-lg text-gray-800">I'll get back to you asap.</p>
        <div class="flex items-center mt-4 text-gray-800">
          <a
            class="flex items-center"
            href="https://www.linkedin.com/in/nikparadis/"
            target="_blank"
          >
            <svg class="h-6 w-6 fill-current text-indigo-600 animate-bounce" viewBox="0 0 26 26">
              <path
                d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"
              />
            </svg>
            <h1 class="px-3 text-lg">My LinkedIn</h1>
          </a>
        </div>
        <div class="flex items-center mt-6 text-gray-800">
          <svg class="h-6 w-6 fill-current text-indigo-600" viewBox="0 0 512 512">
            <path
              d="M256 32c-88.004 0-160 70.557-160 156.801C96 306.4 256 480 256 480s160-173.6 160-291.199C416 102.557 344.004 32 256 32zm0 212.801c-31.996 0-57.144-24.645-57.144-56 0-31.357 25.147-56 57.144-56s57.144 24.643 57.144 56c0 31.355-25.148 56-57.144 56z"
            />
          </svg>
          <h1 class="px-3 text-lg">Waterloo, ON</h1>
        </div>
        <div class="flex items-center my-6 text-gray-800">
          <svg class="h-6 w-6 fill-current text-indigo-600" viewBox="0 0 512 512">
            <path
              d="M437.332 80H74.668C51.199 80 32 99.198 32 122.667v266.666C32 412.802 51.199 432 74.668 432h362.664C460.801 432 480 412.802 480 389.333V122.667C480 99.198 460.801 80 437.332 80zM432 170.667L256 288 80 170.667V128l176 117.333L432 128v42.667z"
            />
          </svg>
          <a
            class="px-3 text-lg items-center"
            href="mailto:nparadis@uwaterloo.ca"
          >nparadis@uwaterloo.ca</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  transition: "fade"
};
</script>
