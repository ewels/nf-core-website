<script lang="ts">
    interface Props {
        date: Date;
        date_options?: Intl.DateTimeFormatOptions;
        showTimezone?: boolean;
    }

    let {
        date = $bindable(),
        date_options = {
            year: "numeric",
            month: "long",
            day: "numeric",
            hour: "numeric",
            minute: "numeric",
            hour12: false,
        },
        showTimezone = false,
    }: Props = $props();
    // don't show time and don't convert to local time if it date includes "00:00:00"
    if (date.toISOString().includes("00:00:00")) {
        date_options.hour = undefined;
        date_options.minute = undefined;
        date_options.timeZone = "UTC";
    }

    // Get user's local timezone
    const userTimezone = Intl.DateTimeFormat().resolvedOptions().timeZone;
</script>

<span>
    {date.toLocaleString("en-US", date_options)}
    {#if showTimezone}
        in {userTimezone}
    {/if}
</span>
