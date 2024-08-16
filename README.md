//# Playwright-project1
import { test, expect } from '@playwright/test';

const username = 'your facebook username';
const password = 'your facebook password';
const postText = 'This is a test post';

test.describe('Facebook', () => {
  test.use({ retries: 2 });

  test.timeout(4 * 1000);

  test('should login successfully', async ({ page }) => {
    await page.goto('(link unavailable)');
    await page.fill('input[name="email"]', username);
    await page.fill('input[name="pass"]', password);
    await page.click('button[name="login"]');
    await expect(page).toHaveURL('(link unavailable)');
  });

  test('should create a new post', async ({ page }) => {
    await page.goto('(link unavailable)');
    await page.click('textarea[aria-label=" This is my First Post "]');
    await page.fill('textarea[aria-label=" This is my First Post  "]', postText);
    await page.click('button[type="submit"]');
    await expect(page.locator('text=' + postText)).toBeVisible();
  });

  test('should display user profile information', async ({ page }) => {
    await page.goto('(link unavailable)' + username);
    await expect(page.locator('text=' + username)).toBeVisible();
    await expect(page.locator('text=Friends')).toBeVisible();
    await expect(page.locator('text=Photos')).toBeVisible();
  });

  test('should search for a friend', async ({ page }) => {
    await page.goto('(link unavailable)');
    await page.fill('input[type="search"]', 'friend_name');
    await page.click('button[type="submit"]');
    await expect(page.locator('text=friend_name')).toBeVisible();
  });

  test('should log out successfully', async ({ page }) => {
    await page.goto('(link unavailable)');
    await page.click('button[aria-label="Account"]');
    await page.click('button[aria-label="Log Out"]');
    await expect(page).toHaveURL('(link unavailable)');
  });
});
