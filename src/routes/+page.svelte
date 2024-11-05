<script>
	import { onMount } from 'svelte';
	
	const images = [
	  '/static/example.jpg',
	  '/static/example2.jpg',
	  '/static/example3.jpg'
	];
	
	let currentImage = 0;
	let showSchedulePopup = false;
	let showProjectPopup = false;
	let currentProjectIndex = 0;
	let currentSlide = 0;
	
	const projects = [
    {
      title: "Modern Kitchen Renovation",
      description: "Complete kitchen transformation featuring custom cabinets, marble countertops, and state-of-the-art appliances. Our team worked closely with the homeowners to create a stunning, functional space that exceeds expectations.",
      images: [
        '/work1/i1.jpg',
        '/work1/i2.jpg',
        '/work1/i3.jpg',
        '/work1/i4.jpg',
        '/work1/i5.jpg',
        '/work1/i6.jpg'
      ]
    },
	  {
		title: "Modern Exterior Renovation ",
		description: "From 90s to future",
		images: [
        '/work2/i1.jpg',
        '/work2/i2.jpg'
      ]
	  }
	];
	
	const reviews = [
	  {
		name: 'No reviews yet',
		rating: 0,
		text: 'N/A'
	  },
	
	];
	
	onMount(() => {
	  const interval = setInterval(() => {
		currentImage = (currentImage + 1) % images.length;
	  }, 5000);
	  
	  return () => clearInterval(interval);
	});
	
	function toggleSchedulePopup() {
	  showSchedulePopup = !showSchedulePopup;
	}
  
	function openProject(index) {
	  currentProjectIndex = index;
	  currentSlide = 0;
	  showProjectPopup = true;
	}
  
	function nextImage() {
	  const currentProject = projects[currentProjectIndex];
	  currentSlide = (currentSlide + 1) % currentProject.images.length;
	}
  
	function previousImage() {
	  const currentProject = projects[currentProjectIndex];
	  currentSlide = (currentSlide - 1 + currentProject.images.length) % currentProject.images.length;
	}
  </script>
  
  <main class="min-h-screen bg-gray-900 text-gray-100">
	<!-- Hero Section -->
	<section class="relative h-[90vh] overflow-hidden">
	  <div class="absolute inset-0 transition-opacity duration-700">
		<img src={images[currentImage]} alt="Remodeling showcase" class="w-full h-full object-cover" />
		<div class="absolute inset-0 bg-black/60 backdrop-blur-sm" />
	  </div>
	  <div class="absolute inset-0 flex flex-col items-center justify-center px-4">
		<h1 class="text-6xl font-bold text-white mb-6">Modern Living Spaces</h1>
		<p class="text-xl text-white/90 mb-8">Crafting Your Dream Home</p>
		<button 
		  on:click={toggleSchedulePopup}
		  class="bg-white text-gray-900 px-8 py-4 rounded-full hover:bg-gray-200 transition-all duration-300 text-lg font-medium"
		>
		  Start Your Project
		</button>
	  </div>
	</section>
  
	<!-- Services Grid -->
	<section class="max-w-7xl mx-auto px-4 py-24">
	  <h2 class="text-4xl font-bold text-center mb-16 text-white">Our Expertise</h2>
	  <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
		{#each ['Kitchen', 'Bathroom', 'Full Home'] as service}
		  <div class="group relative overflow-hidden rounded-2xl bg-gray-800 p-8 shadow-lg hover:shadow-xl transition-all duration-300 border border-gray-700">
			<h3 class="text-2xl font-semibold mb-4 text-white">{service}</h3>
			<p class="text-gray-300">Premium {service.toLowerCase()} remodeling solutions tailored to your style and needs.</p>
		  </div>
		{/each}
	  </div>
	</section>
  
	<!-- Project Gallery -->
	<section class="max-w-7xl mx-auto px-4 py-24">
	  <h2 class="text-4xl font-bold text-center mb-16 text-white">Our Projects</h2>
	  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
		{#each projects as project, i}
		  <div class="group relative aspect-square overflow-hidden rounded-2xl">
			<img 
			  src={project.images[0]} 
			  alt={project.title} 
			  class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-110" 
			/>
			<button 
			  on:click={() => openProject(i)}
			  class="absolute inset-0 bg-black/60 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center"
			>
			  <span class="text-white text-xl font-medium">View Project</span>
			</button>
		  </div>
		{/each}
	  </div>
	</section>
  
	<!-- Reviews Section -->
	<section class="bg-gray-800 py-24">
	  <div class="max-w-7xl mx-auto px-4">
		<h2 class="text-4xl font-bold text-center mb-16 text-white">Client Stories</h2>
		<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
		  {#each reviews as review}
			<div class="bg-gray-900 p-8 rounded-2xl border border-gray-700">
			  <div class="text-yellow-400 text-xl mb-4">{'★'.repeat(review.rating)}</div>
			  <p class="text-gray-300 mb-4">{review.text}</p>
			  <p class="font-medium text-white">{review.name}</p>
			</div>
		  {/each}
		</div>
	  </div>
	</section>
  
	<!-- Contact Section -->
	<section class="py-24 bg-gray-900">
	  <div class="max-w-7xl mx-auto px-4">
		<div class="text-center">
		  <h2 class="text-4xl font-bold mb-8 text-white">Get In Touch</h2>
		  <div class="space-y-4">
			<p class="text-xl text-gray-300">Phone: (123) 456-7890</p>
			<p class="text-xl text-gray-300">Email: info@yourcompany.com</p>
			<button 
			  on:click={toggleSchedulePopup}
			  class="mt-8 bg-white text-gray-900 px-8 py-4 rounded-full hover:bg-gray-200 transition-all duration-300"
			>
			  Schedule Consultation
			</button>
		  </div>
		</div>
	  </div>
	</section>
  
	<!-- Footer -->
	<footer class="bg-black text-gray-300 py-12">
	  <div class="max-w-7xl mx-auto px-4">
		<div class="grid grid-cols-1 md:grid-cols-3 gap-8">
		  <div>
			<h3 class="text-xl font-bold mb-4 text-white">Contact Us</h3>
			<div class="space-y-2">
			  
			  <p>Phone: Get info Error (500)</p>
			</div>
		  </div>
		  <div>
			<h3 class="text-xl font-bold mb-4 text-white">Quick Links</h3>
			<div class="space-y-2">
			  <a href="#gallery" class="block hover:text-white">Gallery</a>
			  <a href="#contact" class="block hover:text-white">Contact</a>
			</div>
		  </div>
		  <div>
			<h3 class="text-xl font-bold mb-4 text-white">Follow Us</h3>
			<div class="flex space-x-4">
			  <a href="#https://www.facebook.com/profile.php?id=61567220378557" class="hover:text-white">Facebook</a>
			</div>
		  </div>
		</div>
		<div class="mt-8 pt-8 border-t border-gray-800 text-center">
		  <p>© 2024 Grumpy's Remodeling LLC. All rights reserved.</p>
		</div>
	  </div>
	</footer>
  
	<!-- Schedule Popup -->
	{#if showSchedulePopup}
	  <div class="fixed inset-0 bg-black/90 backdrop-blur-sm flex items-center justify-center p-4 z-50" on:click={toggleSchedulePopup}>
		<div class="bg-gray-800 rounded-2xl p-8 max-w-md w-full border border-gray-700" on:click|stopPropagation>
		  <h2 class="text-3xl font-bold mb-6 text-white">Let's Connect</h2>
		  <div class="space-y-4">
			<a 
			  href="tel:+1234567890" 
			  class="block w-full bg-white text-gray-900 text-center py-4 rounded-xl hover:bg-gray-200 transition-colors"
			>
			  Call Now
			</a>
			<a 
			  href="https://forms.google.com/your-form-url" 
			  target="_blank"
			  class="block w-full bg-gray-900 text-white text-center py-4 rounded-xl hover:bg-gray-700 transition-colors border border-gray-700"
			>
			  Schedule Online
			</a>
		  </div>
		  <button 
			class="absolute top-4 right-4 text-2xl text-white hover:opacity-70 transition-opacity"
			on:click={toggleSchedulePopup}
		  >
			×
		  </button>
		</div>
	  </div>
	{/if}
  
	<!-- Project Popup -->
	{#if showProjectPopup}
	  <div 
		class="fixed inset-0 bg-black/90 backdrop-blur-sm flex items-center justify-center p-4 z-50"
		on:click={() => showProjectPopup = false}
	  >
		<div 
		  class="bg-gray-800 rounded-2xl max-w-4xl w-full max-h-[90vh] overflow-hidden border border-gray-700"
		  on:click|stopPropagation
		>
		  <div class="relative h-[60vh]">
			<img 
			  src={projects[currentProjectIndex].images[currentSlide]} 
			  alt="Project view"
			  class="w-full h-full object-cover"
			/>
			<button 
			  class="absolute left-4 top-1/2 -translate-y-1/2 bg-gray-800/90 text-white p-2 rounded-full hover:bg-gray-700/90"
			  on:click={previousImage}
			>
			  ←
			</button>
			<button 
			  class="absolute right-4 top-1/2 -translate-y-1/2 bg-gray-800/90 text-white p-2 rounded-full hover:bg-gray-700/90"
			  on:click={nextImage}
			>
			  →
			</button>
		  </div>
		  <div class="p-8">
			<h3 class="text-2xl font-bold mb-4 text-white">{projects[currentProjectIndex].title}</h3>
			<p class="text-gray-300">{projects[currentProjectIndex].description}</p>
		  </div>
		  <button 
			class="absolute top-4 right-4 text-white text-2xl hover:opacity-70 transition-opacity"
			on:click={() => showProjectPopup = false}
		  >
			×
		  </button>
		</div>
	  </div>
	{/if}
  </main>
  