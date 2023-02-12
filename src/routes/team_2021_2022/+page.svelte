<script lang="ts">
  import TeamPage from "../TeamPage.svelte";

  import { management, chairpeople } from "$lib/content/team_2021_2022.json";
</script>

<TeamPage {management} {chairpeople} />
