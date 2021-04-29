<template>
	<div class="home">
		<div class="container">
			<div class="page-header">
				<h1 class="text-center">QR SVG Creator</h1>
				
			</div>
			
			<form class="form">
				<div class="form-group">
					<label class="col-sm-2 control-label">Value:</label>
					<input v-model="value" class="form-control">
				</div>
			</form>
			<vue-qrcode :value="value" tag="svg" id="qrwrap" :options="{ width: 300, margin: 0, color: { dark: '#000', light: '#fff' } }"></vue-qrcode>
			<div class="btn-wrap">
				<button v-on:click="download" class="btn icon-btn">
					download
				</button>
			</div>
		</div>
	</div>
</template>
<style>
	body {
		background: #eee;
	}
	svg {
		width: 300px;
		height: 300px;
	}
	.btn-wrap {
		margin-top: 20px;
	}
	h1 {
		font-weight: 100;
	}
	.btn {
		padding: 10px 20px;
		border: 0;
		font-size: 16px;
		text-transform: uppercase;
		cursor: pointer;
		background: #0a3d62;
		color: #fff;
	}
	.btn:hover {
		background: #3c6382;
	}
	.container {
		display: block;
		max-width: 600px;
		padding: 50px;
		margin: 50px auto;
		background: #fff;
		box-shadow: 0 5px 10px 0 rgba(0,0,0,0.2);
	}
	.form-group label {
		display: block;
		width: 100%;
		text-align: left;
		margin: 0 0 10px 10px;
		font-size: 14px;
	}
	.form-group input, .form-group textarea {
		display: block;
		width: 100%;
		border: 1px solid #e2e2e2;
		border-radius: 50px;	
		text-align: left;
		padding: 10px;
		margin-bottom: 10px;
	}
</style>
<script>
// @ is an alias to /src
import VueQrcode from '@chenfengyuan/vue-qrcode';

export default {
  name: 'Home',
  components: {
    VueQrcode
  },
  data() {
    return {
      value: 'https://example.com',
      size: 100,
      copy: '',
      copied: 'false'
    }
  },
  methods: {
    downloadCreate: function(filename, text) {
      var element = document.createElement('a');
      element.setAttribute('href', 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(text));
      element.setAttribute('download', filename);
      element.style.display = 'none';
      document.body.appendChild(element);
      element.click();
      document.body.removeChild(element);
    },
    download: function() {
      this.copy = document.getElementById('qrwrap');
      this.downloadCreate("qr.svg",this.copy.innerHTML);
    }
  }
}
</script>
