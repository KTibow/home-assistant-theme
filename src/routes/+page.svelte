<script>
  import iconCreate from "@iconify-icons/ic/add";
  import iconCheck from "@iconify-icons/ic/check";
  import {
    argbFromHex,
    Hct,
    SchemeTonalSpot,
    MaterialDynamicColors,
  } from "@material/material-color-utilities";
  import { Button, ButtonLink, StyleFromScheme, Icon } from "m3-svelte";
  let colorInput;
  let color, schemeLight, schemeDark;
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
  const loadTheme = (e) => {
    const serializeScheme = (scheme) => {
      const out = {};
      for (const color of colors) {
        out[color] = MaterialDynamicColors[color].getArgb(scheme);
      }
      return out;
    };
    color = argbFromHex(e.currentTarget.value);
    schemeLight = serializeScheme(new SchemeTonalSpot(Hct.fromInt(color), false, 0));
    schemeDark = serializeScheme(new SchemeTonalSpot(Hct.fromInt(color), true, 0));
  };
  const genTheme = (light, dark) => {
    const genColorVariable = (name, argb) => {
      const kebabCase = name.replace(/[A-Z]/g, (letter) => `-${letter.toLowerCase()}`);
      const red = (argb >> 16) & 255;
      const green = (argb >> 8) & 255;
      const blue = argb & 255;
      return `      m3-scheme-${kebabCase}: ${red}, ${green}, ${blue}`;
    };
    const theme = `Material:
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
${colors.map(c => c.replace(/[A-Z]/g, (letter) => `-${letter.toLowerCase()}`)).map(c => `  md-sys-color-${c}: rgb(var(--m3-scheme-${c}))`).join("\n")}
`;
    const modeStyle = `  modes:
    light:
${Object.entries(light)
  .map(([name, argb]) => genColorVariable(name, argb))
  .join("\n")}
    dark:
${Object.entries(dark)
  .map(([name, argb]) => genColorVariable(name, argb))
  .join("\n")}`;
    return theme + modeStyle;
  };
</script>

{#if schemeLight}
  <StyleFromScheme lightScheme={schemeLight} darkScheme={schemeDark} />
  <div class="box">
    <Icon icon={iconCheck} width="24" height="24" />
    <p class="m3-font-headline-small">Use your theme</p>
    <div class="buttons">
      <ButtonLink type="tonal" href="https://github.com/KTibow/home-assistant-theme">Leave a star</ButtonLink>
      <Button type="tonal" on:click={() => colorInput.showPicker()}>Try again</Button>
      <Button
        type="filled"
        on:click={() => {
          const theme = genTheme(schemeLight, schemeDark);
          navigator.clipboard.writeText(theme);
        }}
      >
        Copy it
      </Button>
    </div>
  </div>
{:else}
  <div class="box">
    <Icon icon={iconCreate} width="24" height="24" />
    <p class="m3-font-headline-small">Create a theme</p>
    <div class="buttons">
      <Button type="filled" on:click={() => colorInput.showPicker()}>Choose a color</Button>
    </div>
  </div>
{/if}
<input type="color" value={undefined} bind:this={colorInput} on:input={loadTheme} />

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
  p {
    margin: 0;
  }
  input {
    position: absolute;
    opacity: 0;
    pointer-events: none;
  }
</style>
