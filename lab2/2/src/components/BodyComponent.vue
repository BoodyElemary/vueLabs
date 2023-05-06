<template>
  <table
    class="table table-striped table-bordered text-center my-4"
    style="margin-left: 5%"
  >
    <thead>
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>City</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="student in students" :key="student.id">
        <td>{{ student.id }}</td>
        <td>{{ student.name }}</td>
        <td>{{ student.city }}</td>
      </tr>
    </tbody>
    <tfoot class="text-center fs-5">
      <tr>
        <th colspan="5">
          Total Students =
          {{ students.length }}
        </th>
      </tr>
    </tfoot>
  </table>
  <!-- sssssssssssssssssssssssssss -->
  <div v-if="modal" id="myModal" tabindex="-1" role="dialog">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Add Student</h5>
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
        <div class="modal-footer py-2">
          <button
            type="button"
            class="btn btn-primary mx-4"
            data-dismiss="modal"
            @click.prevent="showModal"
          >
            Back
          </button>
          <button
            type="button"
            class="btn btn-primary"
            data-dismiss="modal"
            @click.prevent="addStudent()"
          >
            ADD
          </button>
        </div>
      </div>
    </div>
  </div>
  <!-- ddddddddddddddddddddddddddddddddd -->
  <div class="row justify-content-center my-1">
    <button class="btn btn-primary col-4" @click="showModal">Add Student</button>
  </div>
</template>

<script>
import students from "@/students";
import Modal from "./Modal.vue";

export default {
  components: {
    Modal,
  },
  mounted() {
    console.log(this.students);
  },
  data: () => ({
    students: students.students,
    modal: false,
    studentId: "",
    studentName: "",
    studentCity: "",
  }),
  methods: {
    addStudent() {
      if (
        this.studentId == "" ||
        this.studentCity == "" ||
        this.studentName == ""
      ) {
        alert("Enter Student data !!");
      } else {
        let student = {
          id: this.studentId,
          name: this.studentName,
          city: this.studentCity,
        };
        this.students.push(student);
        this.modal = !this.modal;
      }
    },
    showModal() {
      this.modal = !this.modal;
    },
  },
};
</script>

<style>
#myModal {
  position: absolute;
  top: 20%;
  width: 600px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: opacity 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>