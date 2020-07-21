<template>
  <div class="hello">
    <wiki :msg="msg" />
  </div>
</template>

<script>
import wiki from "@/pages/Wiki/components/wiki";
export default {
  name: "index",

  components: {
    wiki
  }
};
</script>


