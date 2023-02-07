<script>
  import { getContext } from "svelte";
  import OutClick from "svelte-outclick";

  let active = false;

  const { styleable } = getContext("sdk");
  const component = getContext("component");
</script>

<div use:styleable={$component.styles}>
  <OutClick on:outclick={() => (active = false)}>
    <button
      on:click={() => (active = !active)}
      type="button"
      class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM"
    >
      <svg
        class="spectrum-Icon spectrum-UIIcon-ChevronDown100 spectrum-Accordion-itemIndicator"
        focusable="false"
        aria-hidden="true"
      >
        <use xlink:href="#spectrum-css-icon-Chevron100" />
      </svg></button
    >

    {#if active === true}
      <div class="dropdown-memnu-container">
        <slot />
      </div>
    {/if}
  </OutClick>
</div>

<style>
  .dropdown-memnu-container {
    z-index: 9999;
    position: absolute;
    background-color: white;
    padding: 10px;
    margin-top: 5px;
    border-radius: 4px;
    border-style: solid;
    border-color: rgb(177, 177, 177);
    border-width: 1px;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
  }
</style>
