<script>
  import "bubbles-ui/css/app.css";

	import { Header, Row, Column100, Card, Table, TableRow, TableCell } from 'bubbles-ui';
//	$: locations = localStorage.getItem('locations');.
let locations = []
</script>

<Header
	title="Locations"
	buttons={[
		{
			icon: 'add',
			color: 'gray-lighter',
			href: '/locations/new'
		}
	]}
/>

<Row>
	<Column100>
		<Card>
			<Table>
				{#each locations as location}
					<TableRow>
						<TableCell
							text={location.name}
							caption={isDevMode() ? location.id : null}
							bold={true}
							href={`locations/${location.id}`}
						/>
						<!-- <TableCell
              align="right"
              tag={{ label: location.status, color: location.status === "closed" ? "error-lightest" : "success-lightest" }}
            /> -->
						<TableCell button={{ href: `locations/${location.id}` }} width="min" />
					</TableRow>
				{:else}
					<TableRow>
						<TableCell
							><p>
								You do not have any locations. You can <a href="/locations/new">create one here</a>.
							</p></TableCell
						>
					</TableRow>
				{/each}
			</Table>
		</Card>
	</Column100>
</Row>
