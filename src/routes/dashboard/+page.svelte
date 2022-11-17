<script>
	import { Header, Row, Spinner, Tag } from 'bubbles-ui';
	let loading = null;

	import icon_locations from '$lib/images/apps/locations-icon.svg';

	let apps = [
		{
			name: 'Locations',
			href: import.meta.env.VITE_APPS_LOCATIONS || '/dashboard/sales',
			icon: icon_locations,
			id: 'locations',
			active: true,
			hidden: false
		}
	];
</script>

<Header title="PackageX Cloud" breadcrumbs={true} />

<section>
	<Row>
		<div class="grid">
			{#each apps as app (app.id)}
				<div class="grid-items">
					<div class="flex">
						<div class="card__wrapper">
							<!-- <Card px={0} py={0} background={null}> -->
							<div class="app__container">
								<div class="img">
									<a
										href={app.href}
										on:click={() => {
											if (app.active) {
												loading = app.id;
											}
										}}
									>
										{#if loading === app.id}
											<div class="spinner__container">
												<Spinner size={3} />
											</div>
										{/if}
										<img
											src={app.icon}
											alt={app.name}
											loading="lazy"
											class:inactive={!app.active}
											class:loading={loading === app.id}
											class="loading"
										/>
									</a>
								</div>
							</div>
							<!-- </Card> -->
						</div>
						<div class="desc">
							<h6>
								{app.name}
							</h6>

							{#if !app.active}
								<Tag label="Contact Sales" color="warning-lightest" />
							{:else if app.tag}
								<Tag {...app.tag} />
							{:else}
								<span class="empty-tag-placeholder" />
							{/if}
						</div>
					</div>
				</div>
			{/each}
		</div>
	</Row>
</section>

<style>
	div.grid {
		display: grid;
		transition: all 1s ease;
		justify-content: space-between;
		grid-template-columns: auto auto auto;
	}
	div.grid-items {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		transition: all 0.1s ease;
		transition: transform 0.4s;
		width: 100%;
		padding: 20px;
	}

	.card__wrapper {
		transition: all 0.4s ease-in-out;
		filter: drop-shadow(0 0 1rem rgb(0 0 0 0.5rem));
	}

	.card__wrapper:hover {
		transform: scale(1.1);
		cursor: pointer;
	}

	.app__container {
		position: relative;
		border-radius: 23%;
		background: var(--white);
		width: -webkit-fill-available;
		box-shadow: rgb(227 230 236 / 65%) 0px 0px 6.875rem;
	}

	:global(html.dark) .app__container {
		background: var(--theme-dark);
		box-shadow: rgb(0 0 0 / 25%) 0px 0px 2rem;
	}

	span.empty-tag-placeholder {
		height: 1.5rem;
	}

	section {
		margin-top: 4rem;
	}
	h6 {
		margin-top: 1.25rem;
		margin-bottom: 0.5rem;
	}

	.flex {
		display: flex;
		flex-direction: column;
		width: 100%;
		height: 100%;
		justify-content: space-between;
		text-align: center;
	}

	img {
		width: 100%;
		height: 100%;
		object-fit: contain;
		border-radius: 23%;
	}

	.img {
		width: 100%;
		flex-grow: 1;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.spinner__container {
		width: 50%;
		height: 50%;
		margin: auto;
		position: absolute;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	/* .img img.loading {
		visibility: hidden;
	} */

	.desc {
		display: flex;
		width: 100%;
		align-items: center;
		flex-direction: column;
	}

	.inactive {
		filter: grayscale(100%);
	}
</style>
