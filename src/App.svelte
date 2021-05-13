<script>
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
	let data = [];
	const options = {
		method: 'GET',
		mode: 'no-cors'
		};
	
	onMount(async () => {
		fetch(apiURL, options)
		.then(response => response.json())
		.then(data => {console.log(data);}).catch(error => {
			console.log(error);
			return [];
		});
	});
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
			{#each data as item }
            <div>
                <p> {item.name} </p>
            </div>
        {/each}
			<!-- {#each apiData.name as hubbleImageName}
			<Card class="mb-3">
				<CardHeader>
					<CardTitle>{apiData.name}</CardTitle>
				</CardHeader>
				<CardBody>
					<img src="" alt="">
				</CardBody>
			</Card>
			{/each} -->
		</Row>
	</Container>
</main>