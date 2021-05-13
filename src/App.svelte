<script>
	import { error } from "console";
import { onMount } from "svelte";
	import {
	  Collapse,
	  Navbar,
	  NavbarToggler,
	  NavbarBrand,
	  Nav,
	  NavItem,
	  NavLink,
	  Container,
	  Row,
	  Col,
	  Card,
	  CardBody,
	  CardHeader,
	  CardTitle,
	} from 'sveltestrap';
  
	let isOpen = false;
	const toggle = () => (isOpen = !isOpen);
	const apiURL = "https://hubblesite.org/api/v3/images/all";
	let data = ([]);
	const options = {
		method: 'GET',
		mode: 'no-cors'
		};
	
	async function getHubbleData() {
		let response = await fetch(apiURL, options);
		let data = await response.json();
		return data;
	}
	const promise = getHubbleData();
	
</script>
  
  <Navbar color="dark" dark>
	<NavbarBrand href="/" class="mr-auto">Hubble Image App</NavbarBrand>
	<NavbarToggler on:click={toggle} className="mr-2" />
	<Collapse {isOpen} navbar>
	  <Nav navbar>
		<NavItem>
		  <NavLink href="/">Home</NavLink>
		</NavItem>
		<NavItem>
		  <NavLink href="#about">About</NavLink>
		</NavItem>
	  </Nav>
	</Collapse>
  </Navbar>

 <main>
	 <Container>
		 <Row>
		{#await promise}
			<p>Loading...</p>
		{:then data}
			{#each data as item}
			<p>Image name: {item.name}</p>
			{/each}
		{:catch error}
			<p stlye="color: red">{error.message}</p>
		{/await}
		</Row>
	</Container>
</main>