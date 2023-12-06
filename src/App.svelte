<script>
	import Table from './Table.svelte';
	
	

	const headers = [
	  { key: "name", value: "Pokemon Name" },
	  { key: "type", value: "Type" },
	  { key: "level", value: "Level" },
	  { key: "ability", value: "Ability" },
	];
  
	const rows = [
	  {
		id: "pikachu",
		name: "Pikachu",
		type: "Electric",
		level: 25,
		ability: "Static",
	  },
	  {
		id: "charizard",
		name: "Charizard",
		type: "Fire/Flying",
		level: 50,
		ability: "Blaze",
	  },
	  {
		id: "bulbasaur",
		name: "Bulbasaur",
		type: "Grass/Poison",
		level: 15,
		ability: "Overgrow",
	  },
	  {
		id: "squirtle",
		name: "Squirtle",
		type: "Water",
		level: 20,
		ability: "Torrent",
	  },
	  {
		id: "jigglypuff",
		name: "Jigglypuff",
		type: "Normal/Fairy",
		level: 18,
		ability: "Cute Charm",
	  },
	  {
		id: "eevee",
		name: "Eevee",
		type: "Normal",
		level: 30,
		ability: "Adaptability",
	  },
	];



</script>

<Table {headers} {rows}>
  <span slot="name" let:headers>{headers}</span>
  <strong slot="level" let:rows>{rows} </strong>
  <span slot="type" let:rows>{rows}</span>
  <span slot="ability" let:rows>{rows}</span>
  
  </Table>