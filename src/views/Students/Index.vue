<script>
import axios from "axios";

export default {
    data() {
        return {
            students: [],
        };
    },

    mounted() {
        this.getStudents();
    },
    
    methods: {

        deleteStudent(id) {
            axios
                .delete("http://laravel-rest-api.test/api/students/" + id)
                .then((response) => {
                    alert(response.data.message);
                    this.getStudents();
                });
        },

        getStudents() {
            axios
                .get("http://laravel-rest-api.test/api/students")
                .then((response) => {
                    this.students = response.data;
                })
        },
    },
};



</script>

<template>
        <!-- create student button -->
                <div class="flex justify-end mb-4">
                        <router-link
                                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                                to="/students/create"
                        >
                                Create Student
                        </router-link>
                </div>
        <table class="min-w-full border-collapse block md:table">
		<thead class="block md:table-header-group">
			<tr class="border border-grey-500 md:border-none block md:table-row absolute -top-full md:top-auto -left-full md:left-auto  md:relative ">
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">ID</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Name</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Course</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Email</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Mobile</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Created at</th>
				<th class="bg-gray-600 p-2 text-white font-bold md:border md:border-grey-500 text-left block md:table-cell">Actions</th>
			</tr>
		</thead>
		<tbody class="block md:table-row-group">
			<tr v-for="(student, index) in students.data" :key="index">
                                <td class="border border-grey-500 p-2 block md:table-cell">{{ student.id }}</td>
                                <td class="border border-grey-500 p-2 block md:table-cell">{{ student.name }}</td>
                                <td class="border border-grey-500 p-2 block md:table-cell">{{ student.course }}</td>
                                <td class="border border-grey-500 p-2 block md:table-cell">{{ student.email }}</td>
                                <td class="border border-grey-500 p-2 block md:table-cell">{{ student.phone }}</td>
                                <td class="border border-grey-500 p-2 block md:table-cell">{{ student.created_at }}</td>
                                <td class="border border-grey-500 p-2 block md:table-cell space-x-2">
                                    <router-link :to="{ path: '/students/' + student.id + '/edit' }" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
                                        Edit
                                    </router-link>
                                    <button @click="deleteStudent(student.id)" class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded">
                                        Delete
                                    </button>
                                </td>
                        </tr>
		</tbody>
	</table>
</template>
      