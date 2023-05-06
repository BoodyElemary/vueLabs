<template>
  <div v-if="flag" id="myModal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Add Student</h5>
          <button
            type="button"
            class="close"
            data-dismiss="modal"
            aria-label="Close"
          >
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form>
            <div class="form-group">
              <label for="studentId">Student ID</label>
              <input
                type="text"
                class="form-control"
                id="studentId"
                v-model.trim="studentId"
              />
            </div>
            <div class="form-group">
              <label for="studentName">Student Name</label>
              <input
                type="text"
                class="form-control"
                id="studentName"
                v-model.trim="studentName"
              />
            </div>
            <div class="form-group">
              <label for="studentCity">Student City</label>
              <input
                type="text"
                class="form-control"
                id="studentCity"
                v-model.trim="studentCity"
              />
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-primary"
            data-dismiss="modal"
            @click.prevent="addStudent()"
          >
            Add Student
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
  
  <script>
export default {
  data: () => ({
    studentId: "",
    studentName: "",
    studentCity: "",
    flag: false,
  }),
  methods: {
    addStudent() {
      this.$emit("add-student", {
        id: this.studentId,
        name: this.studentName,
        city: this.studentCity,
      });
      this.studentId = "";
      this.studentName = "";
      this.studentCity = "";
    },
  },
};
</script>
  