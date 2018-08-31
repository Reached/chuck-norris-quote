<template>
  <Page class="page" backgroundSpanUnderStatusBar="true">
    <ActionBar flat="true" class="action-bar" title="">
      <ActionItem text="Categories" ios.position="left" icon="res://selection"></ActionItem>
      <ActionItem text="Settings" ios.position="right" icon="res://ic_cog"></ActionItem>
    </ActionBar>

      <StackLayout clas="joke-box">
        <Button @tap="getRandomJoke">Get a new joke</Button>
        <Image src="~/chuck-on-fire.png" stretch="none"></Image>
        <Label class="joke-text" v-if="joke" :textWrap="true" :text="joke.value"></Label>
      </StackLayout>
  </Page>
</template>

<script>
  import Settings from '../Settings';

  export default {
      data() {
          return {
              joke: null
          }
      },
      created() {
          this.getRandomJoke();
      },
      methods: {
          getRandomJoke() {
              fetch(`${Settings.BASE_URL}/jokes/random`, {
                  method: 'GET'
              }).then((result) => {
                  return result.json();
              }).then((response) => {
                  this.joke = response;
                  console.log(response);
              }).catch((error) => {
                  console.log(error);
              });
          }
      }
  }
</script>
