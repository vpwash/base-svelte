<script lang="ts">
  import { onMount } from 'svelte';
  
  let isDarkMode = false;
  
  // Handle theme changes
  $: {
    if (typeof document !== 'undefined') {
      if (isDarkMode) {
        document.documentElement.setAttribute('data-theme', 'dark');
        document.documentElement.classList.add('dark');
      } else {
        document.documentElement.setAttribute('data-theme', 'light');
        document.documentElement.classList.remove('dark');
      }
    }
  }

  onMount(() => {
    // Check system preference
    const darkModeMediaQuery = window.matchMedia('(prefers-color-scheme: dark)');
    isDarkMode = darkModeMediaQuery.matches;
    
    // Listen for changes
    const handleChange = (e: MediaQueryListEvent) => {
      isDarkMode = e.matches;
    };
    
    darkModeMediaQuery.addEventListener('change', handleChange);
    
    return () => {
      darkModeMediaQuery.removeEventListener('change', handleChange);
    };
  });
</script>

<div class="navbar bg-base-200 shadow-sm sticky top-0 z-50">
    <div class="navbar-start">
      <div class="dropdown">
        <div tabindex="0" role="button" class="btn btn-ghost lg:hidden">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"> <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h8m-8 6h16" /> </svg>
        </div>
        <ul
          tabindex="0"
          class="menu menu-sm dropdown-content bg-base-100 rounded-box z-1 mt-3 w-52 p-2 shadow">
          <li><a href="/">Item 1</a></li>
          <li>
            <a href="/">Parent</a>
            <ul class="p-2">
              <li><a href="/">Submenu 1</a></li>
              <li><a href="/">Submenu 2</a></li>
            </ul>
          </li>
          <li><a href="/">Item 3</a></li>
        </ul>
      </div>
      <a href="/" class="btn btn-ghost text-xl"><svg width="180" height="40" viewBox="0 0 180 40" xmlns="http://www.w3.org/2000/svg">
        <style>
          .icon {
            fill: none;
            stroke: #6366f1; /* Indigo-500 */
            stroke-width: 2;
            stroke-linecap: round;
          }
          .text-dark {
            font-family: 'Segoe UI', sans-serif;
            font-size: 18px;
            font-weight: 600;
            fill: #1f2937; /* Gray-800 */
          }
          .text-light {
            font-family: 'Segoe UI', sans-serif;
            font-size: 18px;
            font-weight: 600;
            fill: #f9fafb; /* Light mode text for dark backgrounds */
          }
        </style>
      
        <!-- Waveform icon -->
        <path class="icon" d="
          M10 30 
          L10 10 
          M15 30 
          L15 20 
          M20 30 
          L20 5 
          M25 30 
          L25 15 
          M30 30 
          L30 10 
          M35 30 
          L35 25 
          M40 30 
          L40 12 
        "/>
      
        <!-- Brand Text -->
        <text x="60" y="25" class={isDarkMode ? 'text-light' : 'text-dark'}>SiteName</text>
      </svg>
      </a>
    </div>
    <div class="navbar-center hidden lg:flex">
      <ul class="menu menu-horizontal px-1">
        <li><a href="/">Item 1</a></li>
        <li>
          <details>
            <summary>Parent</summary>
            <ul class="p-2">
              <li><a href="/">Submenu 1</a></li>
              <li><a href="/">Submenu 2</a></li>
            </ul>
          </details>
        </li>
        <li><a href="/">Item 3</a></li>
      </ul>
    </div>
    <div class="navbar-end">
      <label class="flex cursor-pointer gap-2">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round">
          <circle cx="12" cy="12" r="5" />
          <path
            d="M12 1v2M12 21v2M4.2 4.2l1.4 1.4M18.4 18.4l1.4 1.4M1 12h2M21 12h2M4.2 19.8l1.4-1.4M18.4 5.6l1.4-1.4" />
        </svg>
        <input 
          type="checkbox" 
          bind:checked={isDarkMode} 
          class="toggle theme-controller"
          aria-label="Toggle dark mode"
        />
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round">
          <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
        </svg>
      </label>
    </div>
  </div>
