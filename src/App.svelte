<script>
	import {loadStdlib} from '@reach-sh/stdlib'
	const reach = loadStdlib('ALGO')

	let account;
	let balance;
	let fundAmount;

	const connectWallet = async () => {
		await getAccount()
		await getBalance()
	}

	const getAccount = async () => {
		account = await reach.getDefaultAccount()
		console.log(account)
	}

	const getBalance = async () => {
		let rawBalance = await reach.balanceOf(account)
		balance = reach.formatCurrency(rawBalance, 4)
		console.log(balance)
	}

	const fundWallet = async () => {
		await reach.fundFromFaucet(account, reach.parseCurrency(fundAmount))
		await getBalance()
	}
</script>

<main>
	<div>
		<button on:click={connectWallet}>connect wallet</button>
		<div>
			<input bind:value={fundAmount} />
			<button on:click={fundWallet}>fund wallet</button>
		</div>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
