<script lang="ts">
    import Discord from "$lib/assets/svg/discord.svg";
    import Telegram from "$lib/assets/svg/telegram.svg";
    import Github from "$lib/assets/svg/github.svg";
    import Arrow from "$lib/assets/svg/arrow.svg";
    import Gmail from "$lib/assets/svg/gmail.svg";
	import { _ } from "svelte-i18n";

    $: footer = [
        {
            title: $_("footer.design"),
            links: [
                {
                    icon: Arrow,
                    text: "VK",
                    url: "https://vk.com/rodiio",
                },
                {
                    icon: Arrow,
                    text: "Telegram",
                    url: "https://t.me/serhiipll"
                }
            ]
        },
        {
            title: $_("footer.contact-us"),
            links: [
                {
                    icon: Discord,
                    text: "Discord",
                    url: "https://discord.com/",
                },
                {
                    icon: Telegram,
                    text: "Telegram",
                    url: "https://telegram.org/"
                },
                {
                    icon: Gmail,
                    text: "Mail",
                    url: "mailto:white@waltuh.xyz"
                }
            ]
        },
        {
            title: $_("footer.development"),
            links: [
                {
                    icon: Github,
                    text: "GitHub",
                    url: "https://github.com/WaltuhXyz/"
                }
            ]
        }
    ]
</script>

<div class="footer">
    <div class="container">
        <div class="grid">
            {#each footer as column}
                <div class="column">
                    <h4>{column.title}</h4>
                    {#each column.links as link}
                        <a href={link.url}>
                            <div class="link">
                                <img src={link.icon} alt={link.text} />
                                <span>{link.text}</span>
                            </div>
                        </a>
                    {/each}
                </div>
            {/each}
        </div>
        <p>Made by DrupalDoesNotExists and TurtleWalter with ❤️ and ☕.</p>
    </div>
</div>

<style>
    .footer {
        width: 100%;
        background-color: var(--color-black);
        margin-top: 7.56rem;
        padding-bottom: 1.62rem;
    }

    h4 {
        margin-top: 3.06rem;
    }

    .link {
        display: inline-flex;
        margin-top: 0.25em;
    }

    .link > * {
        margin: auto;
        color: var(--color-blurple);
    }

    img {
        padding-right: 0.25rem;
    }

    .column {
        display: flex;
        flex-direction: column;
    }

    p {
        padding-top: 3.62em;
        text-align: center;
    }
</style>
