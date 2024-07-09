<template>
  <div class="max-w-[50] bg-slate-800">
    <nav>
      <ul>
        <li>
          <nuxt-link to="/" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Dashboard">
            <i class="mdi mdi-view-dashboard-outline"></i>
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/components" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Components">
            <i class="mdi mdi-toy-brick-outline"></i>
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/diagrams" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Diagrams">
            <i class="mdi mdi-sitemap-outline"></i>
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/security" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Security Cases">
            <i class="mdi mdi-security"></i>
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/ethical" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Ethical Hacking">
            <i class="mdi mdi-cctv"></i>
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/swagger" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Swagger Tester">
            <i class="mdi mdi-code-block-braces"></i>
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/" class="block p-3 bg-slate-900 text-slate-100 transition hover:bg-slate-400" title="Documentation">
            <i class="mdi mdi-text-box-search-outline"></i>
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </div>
</template>