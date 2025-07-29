<script lang="ts">
  import iconCheck from "@ktibow/iconset-material-symbols/check";
  import {
    argbFromHex,
    DynamicScheme,
    Hct,
    SchemeTonalSpot,
    Variant,
  } from "@ktibow/material-color-utilities-nightly";
  import { Button, Icon, colors, genCSS } from "m3-svelte";
  import Branding from "./Branding.svelte";

  let css = $state(`@media (prefers-color-scheme: light) {
:root {
color-scheme: light;
}
:root, ::backdrop {
--m3-scheme-background: 249 249 249;
--m3-scheme-on-background: 50 50 50;
--m3-scheme-surface: 249 249 249;
--m3-scheme-surface-dim: 218 218 218;
--m3-scheme-surface-bright: 249 249 249;
--m3-scheme-surface-container-lowest: 255 255 255;
--m3-scheme-surface-container-low: 243 243 243;
--m3-scheme-surface-container: 238 238 238;
--m3-scheme-surface-container-high: 232 232 232;
--m3-scheme-surface-container-highest: 226 226 226;
--m3-scheme-on-surface: 50 50 50;
--m3-scheme-on-surface-variant: 95 95 95;
--m3-scheme-outline: 123 123 123;
--m3-scheme-outline-variant: 178 178 178;
--m3-scheme-inverse-surface: 14 14 14;
--m3-scheme-inverse-on-surface: 157 157 157;
--m3-scheme-primary: 95 95 95;
--m3-scheme-primary-dim: 83 83 83;
--m3-scheme-on-primary: 249 249 249;
--m3-scheme-primary-container: 235 235 235;
--m3-scheme-on-primary-container: 87 87 87;
--m3-scheme-primary-fixed: 235 235 235;
--m3-scheme-primary-fixed-dim: 221 221 221;
--m3-scheme-on-primary-fixed: 68 68 68;
--m3-scheme-on-primary-fixed-variant: 97 97 97;
--m3-scheme-inverse-primary: 255 255 255;
--m3-scheme-secondary: 95 95 95;
--m3-scheme-secondary-dim: 83 83 83;
--m3-scheme-on-secondary: 249 249 249;
--m3-scheme-secondary-container: 226 226 226;
--m3-scheme-on-secondary-container: 82 82 82;
--m3-scheme-secondary-fixed: 226 226 226;
--m3-scheme-secondary-fixed-dim: 212 212 212;
--m3-scheme-on-secondary-fixed: 63 63 63;
--m3-scheme-on-secondary-fixed-variant: 91 91 91;
--m3-scheme-tertiary: 95 95 95;
--m3-scheme-tertiary-dim: 83 83 83;
--m3-scheme-on-tertiary: 249 249 249;
--m3-scheme-tertiary-container: 255 255 255;
--m3-scheme-on-tertiary-container: 98 98 98;
--m3-scheme-tertiary-fixed: 255 255 255;
--m3-scheme-tertiary-fixed-dim: 241 241 241;
--m3-scheme-on-tertiary-fixed: 80 80 80;
--m3-scheme-on-tertiary-fixed-variant: 109 109 109;
--m3-scheme-error: 187 27 27;
--m3-scheme-error-dim: 169 8 16;
--m3-scheme-on-error: 255 247 246;
--m3-scheme-error-container: 254 78 68;
--m3-scheme-on-error-container: 87 0 3;
--m3-scheme-shadow: 0 0 0;
--m3-scheme-scrim: 0 0 0;
--m3-scheme-on-on-primary: 95 95 95;
--m3-scheme-primary-container-subtle: 218 218 218;
--m3-scheme-on-primary-container-subtle: 76 76 76;
--m3-scheme-tertiary-container-subtle: 218 218 218;
--m3-scheme-on-tertiary-container-subtle: 76 76 76;
--m3-scheme-error-container-subtle: 255 207 201;
--m3-scheme-on-error-container-subtle: 158 0 11;
}
}
@media (prefers-color-scheme: dark) {
:root {
color-scheme: dark;
}
:root, ::backdrop {
--m3-scheme-background: 14 14 14;
--m3-scheme-on-background: 229 229 229;
--m3-scheme-surface: 14 14 14;
--m3-scheme-surface-dim: 14 14 14;
--m3-scheme-surface-bright: 44 44 44;
--m3-scheme-surface-container-lowest: 0 0 0;
--m3-scheme-surface-container-low: 19 19 19;
--m3-scheme-surface-container: 25 25 25;
--m3-scheme-surface-container-high: 31 31 31;
--m3-scheme-surface-container-highest: 38 38 38;
--m3-scheme-on-surface: 229 229 229;
--m3-scheme-on-surface-variant: 147 147 147;
--m3-scheme-outline: 117 117 117;
--m3-scheme-outline-variant: 72 72 72;
--m3-scheme-inverse-surface: 249 249 249;
--m3-scheme-inverse-on-surface: 85 85 85;
--m3-scheme-primary: 249 249 249;
--m3-scheme-primary-dim: 235 235 235;
--m3-scheme-on-primary: 95 95 95;
--m3-scheme-primary-container: 160 160 160;
--m3-scheme-on-primary-container: 35 35 35;
--m3-scheme-primary-fixed: 235 235 235;
--m3-scheme-primary-fixed-dim: 221 221 221;
--m3-scheme-on-primary-fixed: 68 68 68;
--m3-scheme-on-primary-fixed-variant: 97 97 97;
--m3-scheme-inverse-primary: 95 95 95;
--m3-scheme-secondary: 198 198 198;
--m3-scheme-secondary-dim: 185 185 185;
--m3-scheme-on-secondary: 64 64 64;
--m3-scheme-secondary-container: 59 59 59;
--m3-scheme-on-secondary-container: 191 191 191;
--m3-scheme-secondary-fixed: 226 226 226;
--m3-scheme-secondary-fixed-dim: 212 212 212;
--m3-scheme-on-secondary-fixed: 63 63 63;
--m3-scheme-on-secondary-fixed-variant: 91 91 91;
--m3-scheme-tertiary: 249 249 249;
--m3-scheme-tertiary-dim: 235 235 235;
--m3-scheme-on-tertiary: 95 95 95;
--m3-scheme-tertiary-container: 235 235 235;
--m3-scheme-on-tertiary-container: 87 87 87;
--m3-scheme-tertiary-fixed: 255 255 255;
--m3-scheme-tertiary-fixed-dim: 241 241 241;
--m3-scheme-on-tertiary-fixed: 80 80 80;
--m3-scheme-on-tertiary-fixed-variant: 109 109 109;
--m3-scheme-error: 255 113 100;
--m3-scheme-error-dim: 218 52 46;
--m3-scheme-on-error: 74 0 2;
--m3-scheme-error-container: 172 12 18;
--m3-scheme-on-error-container: 255 184 176;
--m3-scheme-shadow: 0 0 0;
--m3-scheme-scrim: 0 0 0;
--m3-scheme-on-on-primary: 249 249 249;
--m3-scheme-primary-container-subtle: 44 44 44;
--m3-scheme-on-primary-container-subtle: 171 171 171;
--m3-scheme-tertiary-container-subtle: 44 44 44;
--m3-scheme-on-tertiary-container-subtle: 171 171 171;
--m3-scheme-error-container-subtle: 96 0 4;
--m3-scheme-on-error-container-subtle: 255 137 125;
}
}`);
  let yaml = $state("");
  let colorInput: HTMLInputElement;
  const loadTheme = (e: InputEvent & { currentTarget: HTMLInputElement }) => {
    const color = argbFromHex(e.currentTarget.value);
    const lightScheme = new DynamicScheme({
      variant: Variant.TONAL_SPOT,
      contrastLevel: 0,
      specVersion: "2025",
      sourceColorHct: Hct.fromInt(color),
      isDark: false,
    });
    const darkScheme = new DynamicScheme({
      variant: Variant.TONAL_SPOT,
      contrastLevel: 0,
      specVersion: "2025",
      sourceColorHct: Hct.fromInt(color),
      isDark: true,
    });
    css = genCSS(lightScheme, darkScheme);

    const genColorVariable = (name: string, argb: number) => {
      const kebabCase = name.replaceAll("_", "-");
      const red = (argb >> 16) & 255;
      const green = (argb >> 8) & 255;
      const blue = argb & 255;
      return `      m3-scheme-${kebabCase}: ${red}, ${green}, ${blue}`;
    };
    yaml = `Material:
  primary-background-color: rgb(var(--m3-scheme-background))
  lovelace-background: var(--primary-background-color)
  sidebar-background-color: var(--primary-background-color)
  sidebar-text-color: var(--secondary-text-color)
  app-header-background-color: var(--primary-background-color)
  app-header-text-color: var(--primary-text-color)
  app-header-selection-bar-color: var(--primary-color)
  app-header-edit-background-color: rgb(var(--m3-scheme-primary-container))
  app-header-edit-text-color: rgb(var(--m3-scheme-on-primary-container))
  secondary-background-color: rgb(var(--m3-scheme-surface-container-highest))
  card-background-color: rgb(var(--m3-scheme-surface-container))
  mdc-ripple-color: var(--primary-color)
  input-fill-color: var(--secondary-background-color)
  input-label-ink-color: var(--secondary-text-color)
  input-ink-color: var(--primary-text-color)
  input-dropdown-icon-color: var(--primary-text-color)
  input-idle-line-color: var(--secondary-text-color)
  input-hover-line-color: var(--secondary-text-color)

  primary-text-color: rgb(var(--m3-scheme-on-background))
  secondary-text-color: rgb(var(--m3-scheme-on-surface-variant))
  disabled-text-color: rgb(var(--m3-scheme-outline))

  primary-color: rgb(var(--m3-scheme-primary))
  text-primary-color: rgb(var(--m3-scheme-on-primary))
  mdc-checkbox-ink-color: rgb(var(--m3-scheme-on-primary))
  link-text-color: var(--primary-color)

  light-primary-color: rgb(var(--m3-scheme-primary-container))
  text-light-primary-color: rgb(var(--m3-scheme-on-primary-container))
  accent-color: rgb(var(--m3-scheme-primary-container))
  text-accent-color: rgb(var(--m3-scheme-on-primary-container))

  switch-unchecked-track-color: rgb(var(--m3-scheme-outline))
  switch-unchecked-button-color: rgb(var(--m3-scheme-on-surface-variant))

  divider-color: transparent
  ha-card-background: rgb(var(--m3-scheme-surface-container))
  ha-card-border-color: transparent
  ha-card-border-radius: 1.25rem

  rgb-primary-background-color: var(--m3-scheme-background)
  rgb-primary-text-color: var(--m3-scheme-on-background)
  rgb-primary-color: var(--m3-scheme-primary)
${colors
  .map((c) => c.name.replaceAll("_", "-"))
  .map((c) => `  md-sys-color-${c}: rgb(var(--m3-scheme-${c}))`)
  .join("\n")}
  modes:
    light:
${colors.map((color) => genColorVariable(color.name, color.getArgb(lightScheme))).join("\n")}
    dark:
${colors.map((color) => genColorVariable(color.name, color.getArgb(darkScheme))).join("\n")}`;
  };
</script>

{@html `<${""}style>${css}</${""}style>`}
{#if yaml}
  <div class="box">
    <Icon icon={iconCheck} width="24" height="24" />
    <p class="m3-font-headline-small">Use your theme</p>
    <div class="buttons">
      <Button variant="tonal" onclick={() => colorInput.showPicker()}>Try again</Button>
      <Button
        variant="filled"
        onclick={() => {
          navigator.clipboard.writeText(yaml);
        }}
      >
        Copy it
      </Button>
    </div>
  </div>
{:else}
  <div class="pair">
    <Branding />
    <Button variant="filled" onclick={() => colorInput.showPicker()}>Choose a color</Button>
  </div>
{/if}
<input type="color" value={undefined} bind:this={colorInput} oninput={loadTheme} />

<style>
  .box {
    background-color: rgb(var(--m3-scheme-surface-container));
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1rem;
    padding: 1.5rem;
    border-radius: 1rem;
  }
  :global(.box > svg) {
    color: rgb(var(--m3-scheme-secondary));
  }
  .buttons {
    display: flex;
    margin-top: 0.5rem;
    gap: 0.5rem;
  }
  .pair {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    margin: auto;
  }
  input {
    position: absolute;
    opacity: 0;
    pointer-events: none;
  }
</style>
