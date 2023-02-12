<script lang="ts">
  import TeamPage from "../TeamPage.svelte";

  import { management, chairpeople } from "$lib/content/team_2019_2020.json";
</script>

<TeamPage {management} {chairpeople} />
