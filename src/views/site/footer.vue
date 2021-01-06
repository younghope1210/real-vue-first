<template>
   <v-footer app color="deep-purple accent-3" dense dark absolute :footer="footer"><!--app을 선언해 주어야 알맞은 영역에 붙게된다-->
    <v-spacer></v-spacer>
    <div>{{ footer + '&copy; '  + new Date().getFullYear()  }}</div>
  </v-footer>
</template>
<script>
export default {
  props: ['footer']
}
</script>
