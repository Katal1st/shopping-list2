 <template>
  <div>
      Add a new shop task
    <div @keyup.enter="$emit('create-new-task', task)">
      <input type="text" placeholder="Enter a task name" v-model="task.newTaskTitle" />
      <input type="text" placeholder="Enter a price" v-model="task.newTaskPrice" />
      <input type="text" placeholder="Enter a quantity" v-model="task.newTaskQuantity" />
    </div>
    <button @click="$emit('create-new-task', task)">+</button>
  </div>
</template>

<script>
export default {
  name: "NewTask",
  components: "",
  props: {},
  data() {
    return {
      task: {
        newTaskTitle: "",
        newTaskPrice: "",
        newTaskQuantity: "",
      }
    };
  },
  methods: {
  },
  computed: {}
};
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