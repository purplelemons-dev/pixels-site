<script lang="ts">
	import { FirebaseApp } from 'sveltefire';
	import { initializeApp } from 'firebase/app';
	import { getFirestore } from 'firebase/firestore';
	import { getAuth } from 'firebase/auth';

	// Initialize Firebase
	const app = initializeApp({
		apiKey: 'AIzaSyB92I1E_TbLS8qZFVO5-EaHaJ4s-qHx4lA',
		authDomain: 'pixels-site.firebaseapp.com',
		projectId: 'pixels-site',
		storageBucket: 'pixels-site.appspot.com',
		messagingSenderId: '285243663360',
		appId: '1:285243663360:web:d792abd8958218b1bf64e5',
		measurementId: 'G-Z071ZM2KSW'
	});
	const firestore = getFirestore(app);
	const auth = getAuth(app);
</script>

<FirebaseApp {auth} {firestore}>
	<slot />
</FirebaseApp>
