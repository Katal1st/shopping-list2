<template>
  <div class="task-card my-style">
    <div>
      <h4>Title:{{ model.title }}</h4>
      <p>Cost:{{ model.cost }}$</p>
      <p>Quantity:{{ model.quantity }}</p>
      <p>Sum:{{ sum }}$</p>
    </div>
</template>

<script>

</script>

<style scoped>
.task-card {
  display: flex;
  justify-content: space-between;
  align-items: center;


}
  .task-card__buttons {
  display: flex;
  justify-content: space-between;
}

.task-card__checkbox {
  margin-right:50px;
}
</style>