<script >
import axios from 'axios'

export default {
	name: 'studentCreate',
	data () {
		return {
			errorList: '',
			model: {
				students: {
					name: '',
					course: '',
					email: '',
					phone: '',
				}
			}
		}
	},

	methods: {
		createStudent () {
			var mythis = this;
			axios.post('http://laravel-rest-api.test/api/students', this.model.students)
				.then(res => {
					alert(res.data.message);

					this.model.students = {
						name: '',
						course: '',
						email: '',
						phone: '',
					}

					this.errorList = '';
				})
				.catch( function(error) {
					if (error.response) {

							if (error.response.status == 422){
								mythis.errorList = error.response.data.errors;
							}
						} else if (error.request) {
						console.log(error.request);
						} else {
						console.log('Error', error.message);
						}
				})
		}		
	}

}

</script>

<template>
        <div class="max-w-7xl mx-auto ">
                <div class="w-11/12 p-12 bg-white">
                        <h1 class="text-xl font-semibold text-center">Add Student</h1>
								<div v-if="Object.keys(this.errorList).length > 0" class="bg-red-100 border border-red-400 text-red-700 px-4 py-3 rounded relative" role="alert">
										<ul class="list-disc list-inside">
												<li v-for="(error, index) in this.errorList" :key="index">{{ error[0] }}</li>
										</ul>
								</div>
                                <input id="name" type="text" v-model="model.students.name" name="name" placeholder="Name" autocomplete="name"
                                        class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner" />
                                <input id="course" type="text" v-model="model.students.course" name="course" placeholder="course" autocomplete="course"
                                        class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner" />
                                <input id="email" type="email" v-model="model.students.email" name="email" placeholder="email" autocomplete="email"
                                        class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner" />
                                <input id="phone" type="number" v-model="model.students.phone" name="phone" placeholder="phone" autocomplete="phone"
                                        class="block w-full p-3 mt-2 text-gray-700 bg-gray-200 appearance-none focus:outline-none focus:bg-gray-300 focus:shadow-inner" />
                                <button type="submit"
										@click="createStudent"
                                        class="w-full py-3 mt-6 font-medium tracking-widest text-white uppercase bg-blue-500 shadow-lg focus:outline-none hover:bg-gray-900 hover:shadow-none">
                                        Create
                                </button>
        </div>
</div></template>