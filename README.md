// ==UserScript==
// @name         FreeRice Multiplication Bot
// @namespace    https://github.com/YOURUSERNAME
// @version      1.1
// @description  Automatically answers Multiplication Table questions on FreeRice
// @author       Grok + Community
// @match        https://play.freerice.com/categories/multiplication-table*
// @grant        none
// @license      MIT
// ==/UserScript==

(function() {
    'use strict';

    function getAnswer() {
        const questionEl = document.querySelector('.card-title');
        if (!questionEl) return null;

        const text = questionEl.textContent.trim();
        // Expected format: "12 x 8" or similar
        const match = text.match(/(\d+)\s*[x×]\s*(\d+)/i);
        if (match) {
            return parseInt(match[1]) * parseInt(match[2]);
        }
        return null;
    }

    function clickCorrectAnswer() {
        const answer = getAnswer();
        if (answer === null) return;

        const buttons = document.querySelectorAll('.card-button');
        for (const btn of buttons) {
            if (parseInt(btn.textContent.trim()) === answer) {
                // Small random delay to look human
                setTimeout(() => {
                    btn.click();
                }, 300 + Math.random() * 600);
                return;
            }
        }
    }

    // Run every 800-1200ms
    setInterval(() => {
        clickCorrectAnswer();
    }, 800 + Math.random() * 400);

    // Auto reload every 15-20 seconds to prevent slowdown
    setTimeout(() => {
        location.reload();
    }, 15000 + Math.random() * 5000);

    console.log('%c✅ FreeRice Multiplication Bot loaded!', 'color: green; font-weight: bold');
})();
