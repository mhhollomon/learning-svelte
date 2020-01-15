<script>
    import LinkFarm from './LinkFarm.svelte';
    
    let link_data = [
        {
            "name" : "CSS",
            "id" : "1",
            "url" : "",
            "children" : [
                {
                    "id" : "2",
                    "name" : "BEM",
                    "url" : "bem.org",
                },
                {
                    "id"   : "3",
                    "name" : "CSS Tricks",
                    "url" : "https://css-tricks.com"
                }
            ]
        },
        {
            'name' : 'C++',
            "id" : "4",
            'children' : [
                {
                    "id" : "5",
                    "name" : 'Andrzej\'s C++ blog',
                    "url"  : 'https://akrzemi1.wordpress.com'
                }
            ]
        }
    ];
</script>

<main>
    <LinkFarm data={link_data}/>
</main>
