<script type="text/javascript">
	import Sidebar from '../../../../components/sidebar.svelte'
	import Navbar from '../../../../components/navbar.svelte'
	import { onMount } from 'svelte';
	import {fly, scale} from 'svelte/transition'
	import ApiController from '../../../../ApiController';
	import jquery from 'jquery';
	
	let perum = null
	let status = false

	let getPerum = () => {
		ApiController({
			method:"GET",
			endpoint:`perumahan`
		}).then(response => {
			perum = response.data.data
			status = true
		})
	}

	let addUnit = () => {
		if(jquery('#perumahan').val() == ""){
			alert('Pilih Perumahan!')
			return 0
		}

		let perumahan = jquery('#perumahan').val()
		let no_spk = jquery('#no_spk').val() == "" ? null : jquery('#no_spk').val()
		let target_spk = jquery('#target_spk').val() == "" ? null : jquery('#target_spk').val()
		let mandor = jquery('#mandor').val() == "" ? null : jquery('#mandor').val()
		let blok = jquery('#blok').val() == "" ? null : jquery('#blok').val()
		let no_perumahan = jquery('#no_perumahan').val() == "" ? null : jquery('#no_perumahan').val()
		let unit = jquery('#unit').val() == "" ? null : jquery('#unit').val()
		let lantai = jquery('#lantai').val() == "" ? null : jquery('#lantai').val()
		let type = jquery('#type').val() == "" ? null : jquery('#type').val()
		let harga_unit = jquery('#harga_unit').val() == "" ? null : jquery('#harga_unit').val()
		let pricelist = jquery('#pricelist').val() == "" ? null : jquery('#pricelist').val()
		let mulai_pengerjaan = jquery('#mulai_pengerjaan').val() == "" ? null : jquery('#mulai_pengerjaan').val()
		let target_pengerjaan = jquery('#target_pengerjaan').val() == "" ? null : jquery('#target_pengerjaan').val()
		let selesai_pengerjaan = jquery('#selesai_pengerjaan').val() == "" ? null : jquery('#selesai_pengerjaan').val()
		let keterangan_pengerjaan = jquery('#keterangan_pengerjaan').val() == "" ? null : jquery('#keterangan_pengerjaan').val()
		let mulai_kavling = jquery('#mulai_kavling').val() == "" ? null : jquery('#mulai_kavling').val()
		let target_kavling = jquery('#target_kavling').val() == "" ? null : jquery('#target_kavling').val()
		let selesai_kavling = jquery('#selesai_kavling').val() == "" ? null : jquery('#selesai_kavling').val()
		let keterangan_kavling = jquery('#keterangan_kavling').val() == "" ? null : jquery('#keterangan_kavling').val()
		let notaris = jquery('#notaris').val() == "" ? null : jquery('#notaris').val()
		let nominal_pembayaran_notaris = jquery('#nominal_pembayaran_notaris').val() == "" ? null : jquery('#nominal_pembayaran_notaris').val()
		let tanggal_pembayaran_notaris = jquery('#tanggal_pembayaran_notaris').val() == "" ? null : jquery('#tanggal_pembayaran_notaris').val()
		let pencairan_plafond = jquery('#pencairan_plafond').val() == "" ? null : jquery('#pencairan_plafond').val()
		let tanggal_bestek = jquery('#tanggal_bestek').val() == "" ? null : jquery('#tanggal_bestek').val()
		let nominal_bestek = jquery('#nominal_bestek').val() == "" ? null : jquery('#nominal_bestek').val()
		let tanggal_imb = jquery('#tanggal_imb').val() == "" ? null : jquery('#tanggal_imb').val()
		let nominal_imb = jquery('#nominal_imb').val() == "" ? null : jquery('#nominal_imb').val()
		let tanggal_balik_nama = jquery('#tanggal_balik_nama').val() == "" ? null : jquery('#tanggal_balik_nama').val()
		let nominal_balik_nama = jquery('#nominal_balik_nama').val() == "" ? null : jquery('#nominal_balik_nama').val()
		let tanggal_pln = jquery('#tanggal_pln').val() == "" ? null : jquery('#tanggal_pln').val()
		let nominal_pln = jquery('#nominal_pln').val() == "" ? null : jquery('#nominal_pln').val()
		let tanggal_air = jquery('#tanggal_air').val() == "" ? null : jquery('#tanggal_air').val()
		let nominal_air = jquery('#nominal_air').val() == "" ? null : jquery('#nominal_air').val()
		let tanggal_retensi = jquery('#tanggal_retensi').val() == "" ? null : jquery('#tanggal_retensi').val()
		let foto_unit = jquery('#foto_unit').prop('files').length == 0 ? null : jquery('#foto_unit').prop('files')[0]
		let bukti_notaris = jquery('#bukti_notaris').prop('files').length == 0 ? null : jquery('#bukti_notaris').prop('files')[0]
		let bukti_retensi = jquery('#bukti_retensi').prop('files').length == 0 ? null : jquery('#bukti_retensi').prop('files')[0]

		ApiController({
			method:"POST",
			endpoint:`unit/add`,
			datas:{
				perumahan, no_spk, target_spk, mandor, blok, no_perumahan, unit, lantai, type,
				harga_unit, pricelist, mulai_pengerjaan, target_pengerjaan, selesai_pengerjaan, keterangan_pengerjaan,
				mulai_kavling, target_kavling, selesai_kavling, keterangan_kavling, notaris, tanggal_pembayaran_notaris, nominal_pembayaran_notaris,
				pencairan_plafond, tanggal_bestek, nominal_bestek, tanggal_imb, nominal_imb, tanggal_balik_nama, nominal_balik_nama,
				tanggal_pln, nominal_pln, tanggal_air, nominal_air, tanggal_retensi, foto_unit, bukti_notaris, bukti_retensi
			}
		}).then(response => {
			if(response.data.msg == "Data Unit Added."){
				alert(response.data.msg)
				window.location.href = '/super-admin/kompilasi-perumahan'
			}
		})
	}

	onMount(async () => {
		getPerum()
	})
</script>

<div id="after-login-layout">
	<Navbar/>
	<div class="flex">
		<Sidebar statusPointer="Kompilasi" pagePointer="admin"/>
		<div class="w-80 content">
			{#if status}
			<div class="flex flex-direction-col flex-gap-large" in:fly={{ y: -20, duration: 600 }}>
				<div class="flex flex-direction-col flex-gap-semi-large w-100">
					<div class="flex flex-direction-col flex-gap-semi-small w-100">
						<div class="title-content">Tambah Unit</div>
						<div class="flex flex-gap-regular flex-center-vertical">
							<div class="text-breadcrumb">Data Kompilasi Perumahan</div>
							<img src="/images/icons/Arrow_Right.svg">
							<div class="text-breadcrumb-active">Tambah</div>
						</div>
					</div>
					<div class="card w-70">
						<div class="flex flex-direction-col flex-gap-semi-large">
							<div class="flex flex-gap-regular">
								<div class="flex flex-direction-col flex-gap-small w-20">
									<div class="title-input-nup">Pilih Perum</div>
									<select class="select-nup" id="perumahan">
										<option value="" selected hidden>Pilih Perumahan</option>
										{#each perum as p}
										<option value="{p.kode}">{p.kode}</option>
										{/each}
									</select>
								</div>
							</div>
							<div class="flex flex-gap-regular">
								<div class="flex flex-direction-col flex-gap-small w-50">
									<div class="title-input-nup">No SPK</div>
									<input type="text" name="" class="input-nup" placeholder="no spk.." id="no_spk">
								</div>
								<div class="flex flex-direction-col flex-gap-small w-50">
									<div class="title-input-nup">Target SPK</div>
									<input type="text" name="" class="input-nup" placeholder="target spk.." id="target_spk">
								</div>
							</div>
							<div class="flex flex-gap-regular">
								<div class="flex flex-direction-col flex-gap-small w-100">
									<div class="title-input-nup">Subkon/Mandor</div>
									<input type="text" name="" class="input-nup" placeholder="subkon/mandor.." id="mandor">
								</div>
							</div>
							<div class="flex flex-gap-regular">
								<div class="flex flex-direction-col flex-gap-small w-25">
									<div class="title-input-nup">Blok</div>
									<select class="select-nup" id="blok">
										<option>AA1</option>
										<option>AA2</option>
										<option>AA3</option>
										<option>AA4</option>
										<option>AA5</option>
										<option>AA6</option>
										<option>AA7</option>
										<option>AA8</option>
										<option>AA9</option>
										<option>AA10</option>
									</select>
								</div>
								<div class="flex flex-direction-col flex-gap-small w-komp">
									<div class="title-input-nup">No. Rumah</div>
									<input type="text" name="" class="input-nup" placeholder="lantai.." id="no_perumahan">
								</div>
								<div class="flex flex-direction-col flex-gap-small w-komp">
									<div class="title-input-nup">Lantai</div>
									<input type="text" name="" class="input-nup" placeholder="lantai.." id="lantai">
								</div>
								<div class="flex flex-direction-col flex-gap-small w-komp">
									<div class="title-input-nup">Unit</div>
									<input type="text" name="" class="input-nup" placeholder="unit.." id="unit">
								</div>
								<div class="flex flex-direction-col flex-gap-small w-komp">
									<div class="title-input-nup">Tipe</div>
									<input type="text" name="" class="input-nup" placeholder="tipe.." id="type">
								</div>
							</div>
							<div class="flex flex-direction-col flex-gap-semi-small">
								<div class="title-input-nup">Atur Tarif Unit</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Harga Unit</div>
											<input type="text" name="" class="input-nup" placeholder="harga unit.." id="harga_unit">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Versi Pricelist</div>
											<input type="text" name="" class="input-nup" placeholder="versi pricelist.." id="pricelist">
										</div>
									</div>
								</div>
								<div class="title-input-nup">Waktu Pembangunan</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-31">
											<div class="title-input-nup">Mulai Pembangunan</div>
											<input type="date" name="" class="input-nup" id="mulai_pengerjaan">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-31">
											<div class="title-input-nup">Target Selesai</div>
											<input type="date" name="" class="input-nup" id="target_pengerjaan">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-31">
											<div class="title-input-nup">Selesai Pembangunan</div>
											<input type="date" name="" class="input-nup" id="selesai_pengerjaan">
										</div>
									</div>
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-100">
											<div class="title-input-nup">Keterangan</div>
											<textarea class="input-nup textarea-spec" placeholder="keterangan.." id="keterangan_pengerjaan"></textarea>
										</div>
									</div>
								</div>
								<div class="title-input-nup">Kavling Siap Bangun</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-31">
											<div class="title-input-nup">Mulai Land Clearing</div>
											<input type="date" name="" class="input-nup" id="mulai_kavling">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-31">
											<div class="title-input-nup">Target Selesai</div>
											<input type="date" name="" class="input-nup" id="target_kavling">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-31">
											<div class="title-input-nup">Tanggal Selesai</div>
											<input type="date" name="" class="input-nup" id="selesai_kavling">
										</div>
									</div>
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-100">
											<div class="title-input-nup">Keterangan</div>
											<textarea class="input-nup textarea-spec" placeholder="keterangan.." id="keterangan_kavling"></textarea>
										</div>
									</div>
								</div>
								<div class="flex flex-gap-regular">
									<div class="flex flex-direction-col flex-gap-small w-50">
										<div class="title-input-nup">Nama Notaris</div>
										<input type="text" name="" class="input-nup" placeholder="nama notaris..." id="notaris">
									</div>
									<div class="flex flex-direction-col flex-gap-small w-50">
										<div class="title-input-nup">Nominal Pembayaran Notaris</div>
										<input type="text" name="" class="input-nup" placeholder="nominal pembayaran notaris.." id="nominal_pembayaran_notaris">
									</div>
								</div>
								<div class="flex flex-gap-regular">
									<div class="flex flex-direction-col flex-gap-small w-50">
										<div class="title-input-nup">Tanggal Pembayaran</div>
										<input type="text" name="" class="input-nup" placeholder="tanggal pembayaran.." id="tanggal_pembayaran_notaris">
									</div>
									<div class="flex flex-direction-col flex-gap-small w-50">
										<div class="title-input-nup">Pencairan Plafond KPR</div>
										<input type="text" name="" class="input-nup" placeholder="pencairan plafond kpr.." id="pencairan_plafond">
									</div>
								</div>
								<div class="title-input-nup">Bestek</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Tanggal Pencairan</div>
											<input type="date" name="" class="input-nup" id="tanggal_bestek">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Nominal Pencairan</div>
											<input type="text" name="" class="input-nup" placeholder="nominal pencairan.." id="nominal_bestek">
										</div>
									</div>
								</div>
								<div class="title-input-nup">IMB Split</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Tanggal Pencairan</div>
											<input type="date" name="" class="input-nup" id="tanggal_imb">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Nominal Pencairan</div>
											<input type="text" name="" class="input-nup" placeholder="nominal pencairan.." id="nominal_imb">
										</div>
									</div>
								</div>
								<div class="title-input-nup">Splitzing dan Balik Nama</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Tanggal Pencairan</div>
											<input type="date" name="" class="input-nup" id="tanggal_balik_nama">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Nominal Pencairan</div>
											<input type="text" name="" class="input-nup" placeholder="nominal pencairan.." id="nominal_balik_nama">
										</div>
									</div>
								</div>
								<div class="title-input-nup">PLN</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Tanggal Pencairan</div>
											<input type="date" name="" class="input-nup" id="tanggal_pln">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Nominal Pencairan</div>
											<input type="text" name="" class="input-nup" placeholder="nominal pencairan.." id="nominal_pln">
										</div>
									</div>
								</div>
								<div class="title-input-nup">Air</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Tanggal Pencairan</div>
											<input type="date" name="" class="input-nup" id="tanggal_air">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-50">
											<div class="title-input-nup">Nominal Pencairan</div>
											<input type="text" name="" class="input-nup" placeholder="nominal pencairan.." id="nominal_air">
										</div>
									</div>
								</div>
								<div class="flex flex-gap-regular">
									<div class="flex flex-direction-col flex-gap-small w-40">
										<div class="title-input-nup">Retensi yang Dicairkan</div>
										<input type="date" name="" class="input-nup" id="tanggal_retensi">
									</div>
								</div>
								<div class="title-input-nup">Unggah Berkas</div>
								<div class="card-secondary flex flex-direction-col flex-gap-semi-large">
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-48">
											<div class="title-input-nup">Foto Unit/Rancangan</div>
											<input type="file" class="file-nup" id="foto_unit">
										</div>
										<div class="flex flex-direction-col flex-gap-small w-48">
											<div class="title-input-nup">Bukti Pembayaran Notaris</div>
											<input type="file" class="file-nup" id="bukti_notaris">
										</div>
									</div>
									<div class="flex flex-gap-regular">
										<div class="flex flex-direction-col flex-gap-small w-48">
											<div class="title-input-nup">Bukti Pencairan Retensi</div>
											<input type="file" class="file-nup" id="bukti_retensi">
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
					<div class="flex flex-end-horizontal w-70">
						<div class="w-40 flex flex-gap-regular flex-end-horizontal">
							<button class="btn-outline flex flex-center-vertical flex-gap-small" on:click={() => {
								window.history.back()
							}}><span>Batal</span></button>
							<button class="btn-fill flex flex-center-vertical flex-gap-small" on:click={() => addUnit()}><span>Simpan Unit</span></button>
						</div>
					</div>
				</div>
			</div>
			{/if}
		</div>
	</div>
</div>