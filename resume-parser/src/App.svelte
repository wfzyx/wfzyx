<script>
    import * as jsonData from './cv.json'
    let resume = JSON.parse(JSON.stringify(jsonData));
    let xpr = XPathResult;
    let fopts = { mode : 'no-cors' }
</script>

<link href="https://emoji-css.afeld.me/emoji.css" rel="stylesheet">

<main>
    <h1>
        {resume.basics.name}&nbsp
        <i class="em-svg em-flag-{resume.basics.location.countryCode}"/>
    </h1>
    <h2>{resume.basics.label}</h2>
    <!--h3>Basics</h3-->
    <p>{resume.basics.summary}</p>
    <h3>Contact me! :D</h3>
    <ul class="container">
        <li class="item"><i class="em-svg em-email"/> <a href="mailto:{resume.basics.email}">{resume.basics.email}</a></li>
<li class="item"><i class="em-svg em-iphone"/> <a href="tel:{resume.basics.phone}">{resume.basics.phone}</a></li>
<li class="item"><i class="em-svg em-squid"/> <a href="{resume.basics.profiles[0].url}">{resume.basics.profiles[0].url}</a></li>
    </ul>
    <h2>Work Experience</h2>
    {#each resume.work as xp}
        <hr/>
        <p style="font-weight: bold">{xp.position} @ <a href="{xp.website}">{xp.company}</a> - Period: {xp.startDate} - {xp.endDate === "" ? "Current" : xp.endDate}</p>
        <p>{xp.summary}</p>
        <p>
            {
            fetch( xp.website , fopts )
            .then( res => console.log(res.text) //document.evaluate
            ( '//*[@id="main-content"]/section[1]/section/div/div[1]/img', res, null, xpr.FIRST_ORDERED_NODE_TYPE, null).singleNodeValue )
            }
            
        </p>
        <hr/>
    {/each}
    <h2>Volunteering</h2>
    {#each resume.volunteer as xp}
        <hr/>
        <p>{xp.position} at {xp.organization}({xp.website})</p>
        <p>Period: {xp.startDate} - {xp.endDate === "" ? "Current" : xp.endDate}</p>
        <p>{xp.summary}</p>
        <hr/>
    {/each}
    <h2>Education</h2>
    {#each resume.education as xp}
        <hr/>
        <p>{xp.studyType} in {xp.area} at {xp.institution}</p>
        <p>Period: {xp.startDate} - {xp.endDate === "" ? "Current" : xp.endDate}</p>
        <hr/>
    {/each}
    <h2>Awards</h2>
    {#each resume.awards as xp}
        <hr/>
        <p>{xp.title} at {xp.awarder}</p>
        <hr/>
    {/each}
    <h2>Publications</h2>
    {#each resume.publications as xp}
        <hr/>
        <p>{xp.name} at {xp.publisher}({xp.website})</p>
        <hr/>
    {/each}
    <h2>Skills</h2>
    <ul class="container">
    {#each resume.skills as skill}
        <li class="item">{skill.name}</li>
    {/each}
    </ul>
    <h2>Languages</h2>
    {#each resume.languages as lang}
        <p>{lang.language}: {lang.fluency}</p>
    {/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		margin: 0 auto;
        width: 50%
	}

	h1 {
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}

    .container {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        margin: 0 auto;
    }

    .container .item {
        flex: 1;
    }
    ul {
        list-style-type: none;
    }
</style>
