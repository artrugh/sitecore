## Performance testing

Avoid any **unexpected breakdowns** of your Sitecore solution.

**Performace testing** covers the scope of your entire build.

### Keep testing as close as possible between environments.

1. It verifies that your site:
    - meets **key performance requirements** such as response time, simultaneous users, and the *page/second rate*
    - can handle spikes in usage, accounting for potential high usage days.

2. It allows the team to see how the solution will handle scaling, looking specifically at the functionality of your site at the minimym and maximum load levels.

3. It allows to flush out any potential concurrency issues.

4. It allows to understand your data size requirements, so you can estimate the data storage capabilities of your site.

### Create use scenarios.

- Demostrate the expected usage of your sitecore solution in a particular situation.

- Determine the criteria for a successful test of a particular scenario (max response time, expected *page/second rate* at a given load, identity metrics).

- Develop the specific test.

- Indentify the breakdown of users within each defined scenario.

Follow the steps to succesfully complete **performance testing**.

1. Idendity the tools for collection metrics.
2. Run tests.
    - Implement one or more of the additional test to measure other spects of your build's performance.
3. Compare testing data with success criteria.
4. Determine potencial areas for improvement.
    - As a developer, the goal is to focus on ways to optimize any code hotspots that are identified during the performance test.
5. Repeat steps as necessary.
    - Make adjustments to your build until your solution succesfully manages the requirements indentified in the use-case scenarios.