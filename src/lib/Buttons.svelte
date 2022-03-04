<script>
import Button from './Button.svelte'
</script>

<div>
  <h3>Empty Button</h3>
  <Button />
</div>
<div>
  <h3>Shy Button</h3>
  <Button> I am Shai Lebuf<br /><img src="https://toppng.com/uploads/preview/just-do-it-shia-labeouf-focused-11609577642dzzitkohxg.png" width="100" /> </Button>
</div>
<div>
  <h3>Diabled Button</h3>
  <Button disabled>
    Disabled button
  </Button>
</div>