<script>
	let users = [
		{ id: 1, name: 'darkblue' },
		{ id: 2, name: 'indigo' },
		{ id: 3, name: 'deeppink' },
		{ id: 4, name: 'salmon' },
		{ id: 5, name: 'gold' }
	];

	let openButton;
	let selectedUser = { id: null, name: null };

	function handleRowClick(user) {
		selectedUser = user;
		openButton.click();
	}

	function handleCloseModal() {
		selectedUser = { id: null, name: null };
	}
</script>

<div class="container py-4 px-3 mx-auto">
	<!-- Button trigger modal -->
	<button
		bind:this={openButton}
		type="button"
		class="btn btn-primary"
		data-bs-toggle="modal"
		data-bs-target="#userBackdrop"
	>
		New User
	</button>

	<!-- Modal -->
	<div
		class="modal fade"
		id="userBackdrop"
		data-bs-backdrop="static"
		data-bs-keyboard="false"
		tabindex="-1"
		aria-labelledby="userBackdropLabel"
		aria-hidden="true"
	>
		<div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title fs-5" id="userBackdropLabel">User Form</h1>
					<button
						type="button"
						class="btn-close"
						data-bs-dismiss="modal"
						aria-label="Close"
						on:click={handleCloseModal}
					></button>
				</div>
				<div class="modal-body">
					<form>
						{#if selectedUser.id}
							<div class="mb-3">
								<label for="exampleInputEmail1" class="form-label">Id</label>
								<input
									id="exampleInputEmail1"
									type="text"
									class="form-control"
									disabled
									bind:value={selectedUser.id}
								/>
							</div>							
						{/if}
						<div class="mb-3">
							<label for="exampleInputPassword1" class="form-label">Name</label>
							<input
								id="exampleInputPassword1"
								type="text"
								class="form-control"
								bind:value={selectedUser.name}
							/>
						</div>
					</form>
				</div>
				<div class="modal-footer">
					<button
						type="button"
						class="btn btn-secondary"
						data-bs-dismiss="modal"
						on:click={handleCloseModal}>Close</button
					>
					<button type="button" class="btn btn-primary">Save</button>
				</div>
			</div>
		</div>
	</div>

	<table class="table table-hover">
		<thead>
			<tr>
				<th scope="col">#</th>
				<th scope="col">Name</th>
			</tr>
		</thead>
		<tbody>
			{#each users as user (user.id)}
				<tr on:click={(_) => handleRowClick(user)}>
					<th scope="row">{user.id}</th>
					<td>{user.name}</td>
				</tr>
			{/each}
		</tbody>
	</table>
</div>

<style lang="scss">
	.table {
		td {
			cursor: pointer;
		}
	}
</style>
