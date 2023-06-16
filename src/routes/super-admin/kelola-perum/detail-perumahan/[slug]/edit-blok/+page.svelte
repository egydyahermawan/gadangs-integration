<script type="text/javascript">
	import Sidebar from '../../../../../../components/sidebar.svelte'
	import Navbar from '../../../../../../components/navbar.svelte'
	import { onMount } from 'svelte';
	import {fly, scale} from 'svelte/transition'
	import ApiController from '../../../../../../ApiController'
	export let data

	let idPerumahan = data.params.slug 

	console.log(idPerumahan)
	let form = {
		id_perumahan: idPerumahan,
		blok:'',
		alamat: '',
	}
	
	function handleSubmit() {
		const formData = new FormData();
		formData.append('id_perumahan', form.id_perumahan);
		formData.append('blok', form.blok);
		formData.append('alamat', form.alamat);

		let postBlok = () => {
			ApiController({
				method: "POST",
				endpoint: `perumahan/${idPerumahan}/blok/add`,
				datas: formData
			}).then(response => {
				console.log(response)
			})
		}
		postBlok()
	}

	let getDetailBlok = () => {
		ApiController({
			method: "GET",
			endpoint: `perumahan/${idPerumahan}/blok`
		}).then(response => {
			resultAPI= response.data.data
			form = resultAPI
		})
	}
	onMount(() => {
		getDetailBlok()
	})

</script>

<div id="after-login-layout">
	<Navbar/>
	<div class="flex">
		<Sidebar statusPointer="Kompilasi" pagePointer="admin"/>
		<div class="w-80 content">
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-direction-col flex-gap-semi-large w-100">
					<div class="flex flex-direction-col flex-gap-semi-small w-100">
						<div class="title-content">Edit Blok</div>
						<div class="flex flex-gap-regular flex-center-vertical">
							<div class="text-breadcrumb">Kelola Perum</div>
							<img src="/images/icons/Arrow_Right.svg">
							<div class="text-breadcrumb">Detail</div>
							<img src="/images/icons/Arrow_Right.svg">
							<div class="text-breadcrumb-active">Edit Blok</div>
						</div>
					</div>
					<div class="card w-70">
						<div class="flex flex-direction-col flex-gap-semi-large">
							<div class="flex flex-gap-regular">
								<div class="flex flex-direction-col flex-gap-small w-30">
									<div class="title-input-nup">Nama Blok</div>
									<input type="text" name="" class="input-nup" placeholder="nama blok.." bind:value={form.blok}>
								</div>
							</div>
							<div class="flex flex-gap-regular">
								<div class="flex flex-direction-col flex-gap-small w-100">
									<div class="title-input-nup">Alamat Blok</div>
									<input type="text" name="" class="input-nup" placeholder="alamat blok.." bind:value={form.alamat}>
								</div>
							</div>
						</div>
					</div>
					<div class="flex flex-end-horizontal w-70">
						<div class="w-40 flex flex-gap-regular flex-end-horizontal">
							<a href="/super-admin/kelola-perum/detail-perumahan" class="no-decor"><button class="btn-outline flex flex-center-vertical flex-gap-small"><span>Batal</span></button></a>
							<button class="btn-fill flex flex-center-vertical flex-gap-small" on:click={handleSubmit}><span>Simpan Perubahan</span></button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>