<script>
  import "../node_modules/materialize-css/dist/css/materialize.min.css";
  import "../node_modules/materialize-css/dist/js/materialize.min.js";
  import { Router, Route } from "svelte-routing";
  import { setupI18n, isLocaleLoaded, locale } from "./services/i18n";
  import { derived } from "svelte/store";
  import Home from "./pages/Home.svelte";
  import About from "./pages/About.svelte";
  import Navbar from "./components/Navbar.svelte";
  import { _ } from "./services/i18n";
  import TranslateButton from "./components/TranslateButton.svelte";
  $: if (!$isLocaleLoaded) {
    setupI18n({ withLocale: "jp" });
  }
  M.AutoInit();
</script>

{#if $isLocaleLoaded}
  <Router>
    <Navbar />
    <Route path="/" component={Home} />
    <Route path="/about" component={About} />
  </Router>
  <div class="container right-align" style="margin-top: 30px;">
    <TranslateButton
      value={$locale}
      on:locale-changed={e => setupI18n({ withLocale: e.detail })} />
  </div>
{:else}
  <p>Loading...</p>
{/if}
