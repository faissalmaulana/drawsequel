<script>
    /**
     * @prop {string} the alphabet (in uppercase) to render as SVG
     * @prop {string} [width="24px"] - SVG width
     * @prop {string} [height="24px"] - SVG height
     */
    let { letter, width = "24", height = "24" } = $props();

    /**
     * object that associate with the path D code
     * key object is the alphabet and the value is
     * code path D value
     *
     * @type {Object.<string, string>}
     */
    const alphabets = {
        A: "M11 7a2 2 0 0 0-2 2v8h2v-4h2v4h2V9a2 2 0 0 0-2-2zm0 2h2v2h-2z",
        N: "M9 7v10h2v-5l2 5h2V7h-2v5l-2-5z",
    };

    /**
     * get individual alphabet from {alphabets} object
     *
     * @param letter {string} the alphabet that want to get, if the alphabet is not found it will return empty string
     * @returns {string}
     */
    function getAlphabetCode(letter) {
        for (let alphabet in alphabets) {
            if (alphabet === letter) {
                return alphabets[alphabet];
            }
        }

        return "";
    }
</script>

<svg xmlns="http://www.w3.org/2000/svg" {width} {height} viewBox="0 0 24 24"
    ><path fill="currentColor" d={getAlphabetCode(letter)} /></svg
>
