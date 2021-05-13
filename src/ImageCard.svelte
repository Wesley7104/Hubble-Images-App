<script>
    import {
      Button,
      Card,
      CardBody,
      CardFooter,
      CardHeader,
      CardTitle
    } from 'sveltestrap';

    export let imageName;
    export let imageSource;

  </script>
  
  <Card class="mb-3">
    <CardHeader>
      <CardTitle>{imageName}</CardTitle>
    </CardHeader>
    <CardBody>
        <img src={imageSource} alt={imageName}>
      <Button>Button</Button>
    </CardBody>
    <CardFooter>No Details...</CardFooter>
  </Card>