<template>
  <q-page class="bg-grey-3 column">
    <q-list
      class="bg-white"
      separator
      bordered
    >
      <!--
        Rendering a <label> tag (notice tag="label")
        so QCheckboxes will respond to clicks on QItems to
        change Toggle state.
      -->

      <q-item
        v-for="(task, id) in tasks"
        :key="task.id"
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1' : task.done}"
        clickable
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            class="no-pointer-events"
            color="primary"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title}}</q-item-label>
        </q-item-section>
        <q-item-section
          v-if="task.done"
          side
        >
          <q-btn
            @click.stop="deleteTask(id)"
            dense
            flat
            round
            color="primary"
            icon="delete"
          />
        </q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      tasks: [
        {
          title: 'ready',
          done: false
        },
        {
          title: 'steady',
          done: true
        },
        {
          title: 'go',
          done: false
        }
      ]
    }
  },
  methods: {
    deleteTask (id) {
      this.$q.dialog({
        title: 'Confirm',
        message: 'Sure?',
        cancel: true,
        persistent: true
      }).onOk(() => {
        // console.log('>>>> OK')
        this.tasks.splice(id, 1)
        this.$q.notify({
          message: 'Task Deleted!',
          color: 'red'
        })
      })
    }
  }
}
</script>

<style lang="scss">
.done {
  .q-item__label {
    text-decoration: line-through;
    color: grey;
  }
}
</style>
