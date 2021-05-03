<script>
	import * as reach from '@reach-sh/stdlib/ALGO';

	let account;
	let balance;

	const connectWallet = async () => {
		await getAccount();
		await getBalance();
	}

	const getAccount = async () => {
		account = await reach.getDefaultAccount();
		console.log(account);
	}

	const getBalance = async () => {
		balance = reach.formatCurrency(await reach.balanceOf(account), 4);
		console.log(balance);
	}
</script>

<main>
	<div>
		<button on:click={connectWallet}>Connect Wallet</button>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
