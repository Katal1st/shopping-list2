<template>

  <div>

    <div>

      <div>



        <div class="clickable" @click="showPrice = !showPrice">
          <div class="clickable" @click="showQuantity = !showQuantity">
            <input
              class="clickable"
              :disabled="!editTitle"
              type="text"
              v-model="task.itemTitle"
              @blur.stop="editTitle = false"
            />
          </div>
        </div>



        <button @click="editTitle = !editTitle">
          {{ editTitleButton }}
        </button>

        
      </div>

    </div>



    <div v-show="showPrice">
      <textarea
        :disabled="!editPrice"
        v-model="task.itemPrice"
        @blur.stop="editPrice = false"
      ></textarea>
    </div>

    <div v-show="showQuantity">
      <textarea
        :disabled="!editQuantity"
        v-model="task.itemQuantity"
        @blur.stop="editQuantity = false"
      ></textarea>
    </div>

    {{ task.itemStatus }}
    
    <button
      v-show="showPrice"
      @click="editPrice = !editPrice"
    >
      {{ editPriceButton }}
    </button>

    <button
      v-show="showQuantity"
      @click="editQuantity = !editQuantity"
    >
      {{ editQuantityButton }}
    </button>

    <button @click="setStatusButton">{{ statusButton }}</button>

    <button @click="moveToDeleted">Delete</button>

  </div>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    taskDetails: {
      taskTitle: String,
      taskPrice: String,
      taskQuantity: String,
      taskStatus: String,
      taskId: Number
    }
  },
  data() {
    return {
      showQuantity: false,
      editQuantity: false,
      showPrice: false,
      editPrice: false,
      editTitle: false,
      task: {
        itemTitle: this.taskDetails.taskTitle,
        itemPrice: this.taskDetails.taskPrice,
        itemQuantity: this.taskDetails.taskQuantity,
        itemStatus: this.taskDetails.taskStatus,
        itemId: this.taskDetails.taskId
      }
    };
  },
  methods: {
    setStatusButton() {
      this.task.itemStatus = this.task.itemStatus === "todo" ? "done" : "todo";
    },
    moveToDeleted() {
      this.task.itemStatus = confirm('remove position?') ? "deleted" : "todo";
    }
  },
  updated() {
    this.$emit("task-update", this.task);
  },
  computed: {
    editTitleButton() {
      return this.editTitle ? "save" : "edit title";
    },
    editPriceButton() {
      return this.editPrice ? "save" : "edit price";
    },
    editQuantityButton() {
      return this.editQuantity ? "save" : "edit quantity";
    },
    statusButton() {
      return this.task.itemStatus === "todo" ? "Done" : "Todo";
    },
    sum() {
      return this.itemPrice * this.itemQuantity
    }
  }
};
</script>

<style scoped>
.clickable {
  cursor: pointer;
}

</style>