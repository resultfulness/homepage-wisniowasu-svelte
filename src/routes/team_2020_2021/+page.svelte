<script lang="ts">
  import TeamPage from "../TeamPage.svelte";

  import { management, chairpeople } from "$lib/content/team_2020_2021.json";
</script>

<TeamPage {management} {chairpeople} />
