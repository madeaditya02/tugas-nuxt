<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
        <div class="d-flex align-items-center">
          <h5>Task</h5>
          <select class="form-select ms-4" v-model="category">
            <option value="" selected>Semua tugas</option>
            <option value="Prioritas">Prioritas</option>
            <option value="Penting">Penting</option>
            <option value="Kurang Penting">Kurang Penting</option>
          </select>
        </div>
        <div class="d-flex align-items-center ms-auto">
          <input type="text" class="form-control" placeholder="Search" v-model="searchQuery">
          <div class="d-flex align-items-center ms-4">
            <span class="me-2">View as</span>
            <button class="btn btn-outline-secondary py-1 px-3" @click="isGrid = !isGrid">
              {{ isGrid ? 'Grid' : 'List' }}
            </button>
          </div>
        </div>
      </div>

      <div class="list-task row">
        <CardItem v-for="(task, i) in resultQuery" :key="i" :task="task" :isGrid="isGrid" />
        <!-- <div v-for="(task, i) in tasks" :key="i"
          :class="['item-task d-flex align-items-center border-bottom pt-3 pb-4', isGrid ? 'col-12 col-md-6 col-lg-4' : 'col-12']">
          <input type="checkbox" name="status" id="task" class="me-2 mt-2" :checked="task.isDone" v-model="task.isDone">
          <div :class="['d-flex flex-column', task.isDone ? 'text-decoration-line-through fst-italic' : '']">
            <div class="title-task mb-1">{{ task.title }}</div>
            <div class="description-task small text-muted">{{ task.description }}</div>
          </div>
        </div> -->
      </div>

      <div class="action py-2">
        <a href="#" class="add-button no-underline" v-if="!isCreating" @click="isCreating =
          !isCreating">Add Task</a>
        <div class="add-card" v-else>
          <div class="card mb-2">
            <div class="card-body d-flex flex-column p-0">
              <input class="form-control border-0 mb-2" placeholder="Title" type="text">
              <textarea class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
            </div>
          </div>
          <div class="button-wrapper d-flex">
            <button class="btn btn-primary me-2">Save</button>
            <button class="btn btn-outline-secondary" @click="isCreating =
              !isCreating">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from '@/components/Card/CardItem.vue'
export default {
  components: { CardItem },
  data() {
    return {
      tasks: [
        {
          title: 'Task 1',
          description: 'ini-deskripsi',
          category: 'Prioritas',
          isDone: false
        },
        {
          title: 'Task 2',
          description: 'ini-deskripsi 2',
          category: 'Kurang Penting',
          isDone: false
        },
        {
          title: 'Task 3',
          description: 'ini-deskripsi 3',
          category: 'Kurang Penting',
          isDone: false
        },
        {
          title: 'Task 14',
          description: 'ini-deskripsi 4',
          category: 'Penting',
          isDone: false
        },
        {
          title: 'Task 15',
          description: 'ini-deskripsi 5',
          category: 'Prioritas',
          isDone: false
        },
      ],
      searchQuery: '',
      category: '',
      isCreating: false,
      isGrid: false
    }
  },
  computed: {
    resultQuery() {
      let result = this.tasks.filter(item => this.category ? item.category == this.category : true)
      if (this.searchQuery) {
        return result.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      }
      return result
    }
  },
  layout(context) {
    return 'custom'
  }
}
</script>
