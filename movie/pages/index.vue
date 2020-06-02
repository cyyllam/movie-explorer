<template>
  <section>
    <b-container>
      <Intro>
        <p slot="content">
            It's easy to google for a generic list of the best movies to watch, but sometimes that search can be 
            onerous when you have something more specific in mind. Perhaps you're looking for a list of movies trending
            this week, or maybe a list of movies off the beaten path that matches a set of criteria. Maybe you just want to know, 
            of the films Ryan Gosling has acted in, which have won awards? Look no further, click on <span class='italics'>Trends</span> to get started.
          </p>
      </Intro>
    </b-container>
  </section>
</template>

<script>
import Intro from '~/components/intro.vue'

export default {
  components: {
    Intro

  }
}
</script>

<style>

.italics {
  font-style: italic;
}

</style>

