# Wiley-Test-Automation
Playwright automated test scripts for Wiley Online Library website.
const { test, expect } = require('@playwright/test');

test.describe('Wiley Online Library - Functional Test Automation', () => {

  // Test Case 1: Homepage Loading
  test('Homepage loads successfully with all elements', async ({ page }) => {
    await page.goto('https://onlinelibrary.wiley.com/');
    await expect(page.locator('input#searchField')).toBeVisible(); // Search bar
    await expect(page.locator('nav')).toBeVisible(); // Navigation menu
    await expect(page.locator('.feature-content')).toBeVisible(); // Featured articles
  });

  // Test Case 2: Search Functionality
  test('Search for articles using valid keywords', async ({ page }) => {
    await page.goto('https://onlinelibrary.wiley.com/');
    await page.locator('input#searchField').fill('machine learning');
    await page.locator('button[type="submit"]').click(); // Click search button
    await expect(page).toHaveURL(/search/); // Verify URL contains 'search'
    const results = await page.locator('.search-results__item');
    await expect(results).toHaveCountGreaterThan(0); // Ensure search results are displayed
  });

  // Test Case 3: Login Functionality
  test('User can log in with valid credentials', async ({ page }) => {
    await page.goto('https://onlinelibrary.wiley.com/');
    await page.locator('a[href*="/login"]').click(); // Navigate to login page
    await page.locator('input#email').fill('validUser@example.com'); // Fill in email
    await page.locator('input#password').fill('ValidPassword123'); // Fill in password
    await page.locator('button[type="submit"]').click(); // Click login button
    await expect(page.locator('text=My Dashboard')).toBeVisible(); // Validate dashboard
  });

});
