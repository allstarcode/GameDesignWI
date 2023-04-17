<script lang="ts">
  import ScheduleBlock from './ScheduleBlock.svelte';
  import AllMatsLink from './AllMatsLink.svelte';
  import type { Schedule } from '../index';
  import { allData } from '../data/ScheduleData';

  const data: Schedule = allData;
</script>

<ul class="collapsible">
  {#each data as day}
    <li>
      <div
        id={`LITATF-day-${day.daynum}-header`}
        class="collapsible-header title"
        data-state="closed"
      >
        <span>Day {day.daynum} -</span>
        <span class="dayofWeek">
          &nbsp;
          {#if day.daynum === '1'}
            Saturday
          {:else if day.daynum === '2'}
            Sunday
          {/if}
        </span>
        <span class="titleFix">&nbsp;{day.title}</span>
      </div>
      <div class="collapsible-body">
        {#each day.activities as activity}
          <ScheduleBlock
            name={activity.name}
            time={activity.time}
            duration={activity.duration}
            actType={activity.actType}
            links={activity.links}
            daynum={day.daynum}
          />
        {/each}
      </div>
    </li>
  {/each}
  <li class="litatf-all-links all-links">
    <div class="collapsible-header">
      <div class="title">All Materials</div>
    </div>
    <div class="collapsible-body">
      <ul class="collection">
        {#each data as day}
          {#each day.activities as activity}
            {#if activity.links.length > 0}
              <AllMatsLink
                classes={`day${day.daynum}-all-links`}
                actname={activity.name}
                links={activity.links}
              />
            {/if}
          {/each}
        {/each}
      </ul>
    </div>
  </li>
</ul>
