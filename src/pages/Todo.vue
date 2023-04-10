<template>
  <q-page class="bg-grey-3 column q-pa-xl">
    <div class="row q-pb-xl">

      <q-input filled bg-color="white" v-model="newTask" label="Add task" dense class="col" square @keyup.enter="addTask">

        <template v-slot:append>
          <q-btn round dense flat icon="add" @click="addTask"  />
        </template>
      </q-input>

    </div>
    <q-list separator bordered v-if="tasks.length">
      <q-item tag="label" v-ripple v-for="(task, index) in tasks" :key="index" @click="task.done = !task.done"
        :class="{ ' bg-green-1': task.done }">
        <q-item-section avatar>
          <q-checkbox v-model="task.done" val="teal" color="teal" />
        </q-item-section>
        <q-item-section>
          <q-item-label :class="{ done: task.done }">{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn flat round color="primary" icon="delete" @click="deleteTask(task.title)" />
        </q-item-section>
      </q-item>
    </q-list>
    <div class="no-task absolute-center" v-else>
      <q-icon name="style" color="primary" size="150px"/>
      <div class="text-h4 text-primary text-center">No tasks</div>
    </div>
  </q-page>
</template>

<script>

export default {
  data() {
    return {
      tasks: [
        {
          title: 'Learn JS',
          done: true
        },

      ],
      newTask: ''
    }
  },
  methods: {
    deleteTask(title) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Delete?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        this.tasks = this.tasks.filter((elem) => elem.title != title)
        this.$q.notify({
          message: 'Success',
          icon: 'announcement'
        })
      })
    },
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          done: false
        })
      }

      this.newTask = ""
    }
  }
}
</script>

<style lang="sass">
.done
  text-decoration: line-through
</style>