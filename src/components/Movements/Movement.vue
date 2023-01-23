<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action" @click="remove(id)">
      <img src="@/assets/trash-icon.svg" alt="borrar" />
      <p :class="{ red: isNegative, green: !isNegative }">
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<script setup>
import currencyFormater from "@/js/currencyFormater";
import { toRefs, defineProps, computed, defineEmits } from "vue";

const props = defineProps({
  movement: {
    type: Object,
  },
});

console.log(props);

const { id, title, description, amount } = toRefs(props.movement);

const emit = defineEmits(["remove"]);

const remove = (id) => {
  emit("remove", id);
};

const isNegative = computed(() => amount.value < 0);

const amountCurrency = computed(() => {
  return currencyFormater.format(amount.value);
});
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
  color: red;
}
.green {
  color: green;
}
</style>
