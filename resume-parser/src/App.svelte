<script>
    import * as jsonData from './cv.json'
    let resume = JSON.parse(JSON.stringify(jsonData));
</script>

<link href="https://emoji-css.afeld.me/emoji.css" rel="stylesheet">

<main>
    <h1>{resume.basics.name}</h1><h2>Software Blacksmith and {resume.basics.label}</h2>
    <p>{resume.basics.summary}</p>
    <table style="width: 100%">
        <tr>
            <td><b>Links</b></td>
            <td><div>Email</div><i class="noprint em-svg em-email"/> <a href="mailto:{resume.basics.email}">{resume.basics.email}</a></td>
            <td><div>Phone</div><i class="noprint em-svg em-iphone"/> <a href="tel:{resume.basics.phone}">{resume.basics.phone}</a></td>
            <td><div>Github</div><i class="noprint em-svg em-squid"/> <a href="{resume.basics.profiles[0].url}">{resume.basics.profiles[0].url}</a></td>
        </tr>
        <tr>
            <td colspan=4><hr/></td>
        </tr>
        <tr>
            <td><b>Languages</b></td>
            {#each resume.languages as lang}
                <td><div>{lang.language}</div><i class="noprint em-svg em-flag-{lang.code}"/> {lang.fluency}</td>
            {/each}
        </tr>
    </table>
    <h2><i class="noprint em em-desktop_computer" aria-role="presentation" aria-label=""/> Work Experience</h2>
    <div class="ninja">
        <p>Company: Facebook</p>
        <p>Company: Apple</p>
        <p>Company: Amazon</p>
        <p>Company: Netflix</p>
        <p>Company: Google</p>
    </div>
    {#each resume.work as comp}
        <div class="pagebreak">
        <hr/>
        Company: <a href="{comp.website}">{comp.company}</a>
        <hr/>
        {#each comp.positions as pos, idx}
            {#if idx % 2 === 0} <tr> {/if}
                <td>
                    <p><b>{pos.title} from {pos.startDate} until {pos.endDate === "" ? "today" : pos.endDate}</b></p>
                    <p>{pos.summary}</p>
                </td>
        {/each}
        </div>
    {/each}
    <div class="pagebreak">
    <h2><i class="noprint em em-male-student" aria-role="presentation" aria-label=""/> Education</h2>
        <table style="width:100%">
            {#each resume.education as xp}
            <tr>
                <td><b>{xp.studyType}</b> in {xp.area} at </td>
                <td class="noprint">{xp.institution}</td>
                <td> <b>{xp.acro}</b> </td>
                <td style="text-align: right">from {xp.startDate} until {xp.endDate === "" ? "today" : xp.endDate} </td>
            <tr>
            {/each}
        </table>
    </div>
    <table>
            <tr><td><h3><i class="noprint em em-chart_with_upwards_trend" aria-role="presentation" aria-label="CHART WITH UPWARDS TREND"/> Awards</h3></td> <td><h3><i class="noprint em em-raised_hands" aria-role="presentation" aria-label="PERSON RAISING BOTH HANDS IN CELEBRATION"/> Volunteering</h3></td></tr>
    <tr><td>
        <table>
            {#each resume.awards as xp}
                <tr><td><b>{xp.title}</b> at {xp.awarder}</td></tr>
            {/each}
        </table>
        </td><td>
        <table>
            {#each resume.volunteer as xp}
                <td><b>{xp.position} at <a href="{xp.website}">{xp.organization}</a> from {xp.startDate} until {xp.endDate === "" ? "today" : xp.endDate}</b></td>
                <tr><td>{xp.summary}</td></tr>
            {/each}
        </table>
    </td></tr></table>
    <div class="ninja"> 
    <h2>Skills</h2>
        {#each resume.skills as skill}
            {skill}&nbsp
        {/each}
    </div>
</main>

<style>

	main {
		text-align: justify;
		padding: 1em;
		margin: 0 auto;
		width: 75em;
		line-height: 1.4;
		font-size: x-small;
	}

    td {
        padding: 0 1em 0 0;
    }

	h1 {
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}

    hr {
        margin: 0.5em 0 0.5em 0;
    }

    p {
        margin: 0 0 1em 0;
    }
    .ninja {
        color: transparent;
        font-size: 0.1em;
        float: right;
        position: absolute;
    }
    .noscreen {
        display: none;
    }


    @media print
    {
        .noprint { display: none; }
        .pagebreak { page-break-inside: avoid; }
        .noscreen { display: block; }
        main { width: 50em; }
    }

</style>
