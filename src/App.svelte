<script>
  import Accordion from './lib/Accordion.svelte'
  import Button from './lib/Button.svelte'
  import Buttons from './lib/Buttons.svelte'
  import Editor from './lib/Editor.svelte'
  import Modal from './lib/Modal.svelte'
  import TypeGame from './lib/TypeGame.svelte'
  import { lightTheme } from "./stores/themeStore.js";
  import { faqs } from './faqs'

  /**
   * Sets our current tab
  */
  let currentTab = 'Accordion'

  /**
   * Sets our modal view status
  */
  let showModal = false;

  /**
   * Sets a property called lightTheme to use LocalStorage
  */
  lightTheme.useLocalStorage();

  /**
   * We use $: to set our statement as reactive
   * https://svelte.dev/docs#component-format-script-3-$-marks-a-statement-as-reactive
   * This checks the value of $lightTheme and adds or removes dark-mode to the body
  */
  $: $lightTheme ? document.body.classList.remove('dark-mode') : document.body.classList.add('dark-mode');

  /**
   * Create a property called themeIcon
   * themeIcon is reactive and will change based on the value of $lighttheme
  */
  $: themeIcon = $lightTheme ? '🌙' : '🌞';

  /**
   * Method to toggle our theme
  */
  const toggleTheme = () => $lightTheme = !$lightTheme;
</script>

<header>

  <h1>SveltJS Demo</h1>
  
</header>

<main>
  <Button on:click="{ () => {currentTab = 'Accordion'} }">Accordion</Button>
  <Button on:click="{ () => {currentTab = 'Button'} }">Button</Button>
  <Button on:click="{ () => currentTab = 'Modal' }">Modal</Button>
  <Button on:click="{ () => currentTab = 'Editor' }">Editor</Button>
  <Button on:click="{ () => currentTab = 'TypeGame' }">TypeGame</Button>
  <Button on:click={toggleTheme}>{themeIcon} &nbsp;  Toggle theme</Button>

  <hr /> 

  <h2>Current Tab: <em>{ currentTab }</em></h2>

  <hr />

  {#if currentTab === 'Accordion'}
    <Accordion faqs="{faqs}" />
  {/if}

  {#if currentTab === 'Button'}
    <Buttons />
  {/if}

  {#if currentTab === 'Modal'}
    <Button on:click={() => showModal = true}>modal</Button>

    <Modal {showModal} on:cancel={() => showModal = false} on:close={() => showModal=false}>
      <div slot="header">Modal Header</div>

      <h3>This is a modal</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce ultrices auctor purus, et volutpat nisi interdum non. Nam efficitur lectus non euismod volutpat. Praesent in urna risus.</p>

    </Modal>
  {/if}

  {#if currentTab === 'Editor'}
    <Editor />
  {/if}

  {#if currentTab === 'TypeGame'}
    <TypeGame />
  {/if}
</main>

<style>

  header {
      text-align: center;
  }

  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 1;
  }

  h1 {
    width: 100%;
  }

  :global(body) {
    background-color: #fefefe;
    color: #1d3040;
    transition: all 0.3s;
    min-height: 100vh;
    width: 100%;
  }

  :global(body.dark-mode) {
    background-color: #1d3040;
    color: #fefefe;
  }
</style>