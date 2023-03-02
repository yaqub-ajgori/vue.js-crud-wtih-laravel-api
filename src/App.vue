<template>
  <body>
	<header class="bg-gray-100 py-4">
		<nav class="container mx-auto flex justify-between items-center">
			<div class="logo">Logo</div>
			<ul class="flex items-center">
        <li class="mr-6">
          <router-link class="text-gray-700 hover:text-gray-900" to="/">Home</router-link>
        </li>
        <li class="mr-6">
          <router-link class="text-gray-700 hover:text-gray-900" to="/about">About</router-link>
        </li>
        <li class="mr-6">
          <router-link class="text-gray-700 hover:text-gray-900" to="/students">Students</router-link>
        </li>
			</ul>
		</nav>
	</header>
	<main class="container mx-auto p-2 mt-12">
		<router-view></router-view>
	</main>
</body>
</template>