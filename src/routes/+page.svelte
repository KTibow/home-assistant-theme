<script lang="ts">
  import iconCheck from "@ktibow/iconset-material-symbols/check";
  import { argbFromHex, Hct, SchemeTonalSpot } from "@material/material-color-utilities";
  import { Button, Icon, genCSS, serializeScheme } from "m3-svelte";
  import Branding from "./Branding.svelte";

  let css = $state(`
@media (prefers-color-scheme: light) {
  :root {
    color-scheme: light;
  }
  :root,
  ::backdrop {
    --m3-scheme-primary: 0 0 0;
    --m3-scheme-on-primary: 226 226 226;
    --m3-scheme-primary-container: 59 59 59;
    --m3-scheme-on-primary-container: 255 255 255;
    --m3-scheme-inverse-primary: 198 198 198;
    --m3-scheme-secondary: 94 94 94;
    --m3-scheme-on-secondary: 255 255 255;
    --m3-scheme-secondary-container: 212 212 212;
    --m3-scheme-on-secondary-container: 27 27 27;
    --m3-scheme-tertiary: 59 59 59;
    --m3-scheme-on-tertiary: 226 226 226;
    --m3-scheme-tertiary-container: 116 116 116;
    --m3-scheme-on-tertiary-container: 255 255 255;
    --m3-scheme-error: 186 26 26;
    --m3-scheme-on-error: 255 255 255;
    --m3-scheme-error-container: 255 218 214;
    --m3-scheme-on-error-container: 65 0 2;
    --m3-scheme-background: 249 249 249;
    --m3-scheme-on-background: 27 27 27;
    --m3-scheme-surface: 249 249 249;
    --m3-scheme-on-surface: 27 27 27;
    --m3-scheme-surface-variant: 226 226 226;
    --m3-scheme-on-surface-variant: 71 71 71;
    --m3-scheme-inverse-surface: 48 48 48;
    --m3-scheme-inverse-on-surface: 241 241 241;
    --m3-scheme-outline: 119 119 119;
    --m3-scheme-outline-variant: 198 198 198;
    --m3-scheme-shadow: 0 0 0;
    --m3-scheme-scrim: 0 0 0;
    --m3-scheme-surface-dim: 218 218 218;
    --m3-scheme-surface-bright: 249 249 249;
    --m3-scheme-surface-container-lowest: 255 255 255;
    --m3-scheme-surface-container-low: 243 243 243;
    --m3-scheme-surface-container: 238 238 238;
    --m3-scheme-surface-container-high: 232 232 232;
    --m3-scheme-surface-container-highest: 226 226 226;
    --m3-scheme-surface-tint: 94 94 94;
  }
}
@media (prefers-color-scheme: dark) {
  :root {
    color-scheme: dark;
  }
  :root,
  ::backdrop {
    --m3-scheme-primary: 255 255 255;
    --m3-scheme-on-primary: 27 27 27;
    --m3-scheme-primary-container: 212 212 212;
    --m3-scheme-on-primary-container: 0 0 0;
    --m3-scheme-inverse-primary: 94 94 94;
    --m3-scheme-secondary: 198 198 198;
    --m3-scheme-on-secondary: 27 27 27;
    --m3-scheme-secondary-container: 71 71 71;
    --m3-scheme-on-secondary-container: 226 226 226;
    --m3-scheme-tertiary: 226 226 226;
    --m3-scheme-on-tertiary: 27 27 27;
    --m3-scheme-tertiary-container: 145 145 145;
    --m3-scheme-on-tertiary-container: 0 0 0;
    --m3-scheme-error: 255 180 171;
    --m3-scheme-on-error: 105 0 5;
    --m3-scheme-error-container: 147 0 10;
    --m3-scheme-on-error-container: 255 218 214;
    --m3-scheme-background: 19 19 19;
    --m3-scheme-on-background: 226 226 226;
    --m3-scheme-surface: 19 19 19;
    --m3-scheme-on-surface: 226 226 226;
    --m3-scheme-surface-variant: 71 71 71;
    --m3-scheme-on-surface-variant: 198 198 198;
    --m3-scheme-inverse-surface: 226 226 226;
    --m3-scheme-inverse-on-surface: 48 48 48;
    --m3-scheme-outline: 145 145 145;
    --m3-scheme-outline-variant: 71 71 71;
    --m3-scheme-shadow: 0 0 0;
    --m3-scheme-scrim: 0 0 0;
    --m3-scheme-surface-dim: 19 19 19;
    --m3-scheme-surface-bright: 57 57 57;
    --m3-scheme-surface-container-lowest: 14 14 14;
    --m3-scheme-surface-container-low: 27 27 27;
    --m3-scheme-surface-container: 31 31 31;
    --m3-scheme-surface-container-high: 42 42 42;
    --m3-scheme-surface-container-highest: 53 53 53;
    --m3-scheme-surface-tint: 198 198 198;
  }
}
`);
  let yaml = $state("");
  let colorInput: HTMLInputElement;
  const colors = [
    "primary",
    "onPrimary",
    "primaryContainer",
    "onPrimaryContainer",
    "inversePrimary",
    "secondary",
    "onSecondary",
    "secondaryContainer",
    "onSecondaryContainer",
    "tertiary",
    "onTertiary",
    "tertiaryContainer",
    "onTertiaryContainer",
    "error",
    "onError",
    "errorContainer",
    "onErrorContainer",
    "background",
    "onBackground",
    "surface",
    "onSurface",
    "surfaceVariant",
    "onSurfaceVariant",
    "inverseSurface",
    "inverseOnSurface",
    "outline",
    "outlineVariant",
    "shadow",
    "scrim",
    "surfaceDim",
    "surfaceBright",
    "surfaceContainerLowest",
    "surfaceContainerLow",
    "surfaceContainer",
    "surfaceContainerHigh",
    "surfaceContainerHighest",
    "surfaceTint",
  ];
  const loadTheme = (e: InputEvent & { currentTarget: HTMLInputElement }) => {
    const color = argbFromHex(e.currentTarget.value);
    const lightScheme = new SchemeTonalSpot(Hct.fromInt(color), false, 0);
    const darkScheme = new SchemeTonalSpot(Hct.fromInt(color), true, 0);
    css = genCSS(serializeScheme(lightScheme), serializeScheme(darkScheme));

    const genColorVariable = (name: string, argb: number) => {
      const kebabCase = name.replace(/[A-Z]/g, (letter) => `-${letter.toLowerCase()}`);
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
  .map((c) => c.replace(/[A-Z]/g, (letter) => `-${letter.toLowerCase()}`))
  .map((c) => `  md-sys-color-${c}: rgb(var(--m3-scheme-${c}))`)
  .join("\n")}
  modes:
    light:
${Object.entries(serializeScheme(lightScheme))
  .map(([name, argb]) => genColorVariable(name, argb))
  .join("\n")}
    dark:
${Object.entries(serializeScheme(darkScheme))
  .map(([name, argb]) => genColorVariable(name, argb))
  .join("\n")}`;
  };
</script>

{@html `<${""}style>${css}</${""}style>`}
{#if yaml}
  <div class="box">
    <Icon icon={iconCheck} width="24" height="24" />
    <p class="m3-font-headline-small">Use your theme</p>
    <div class="buttons">
      <Button variant="tonal" click={() => colorInput.showPicker()}>Try again</Button>
      <Button
        variant="filled"
        click={() => {
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
    <Button variant="filled" click={() => colorInput.showPicker()}>Choose a color</Button>
  </div>
{/if}
<input type="color" value={undefined} bind:this={colorInput} oninput={loadTheme} />

<style>
  .box {
    background-color: rgb(var(--m3-scheme-surface-container-high));
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
