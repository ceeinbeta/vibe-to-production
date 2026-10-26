# The Production-Ready Checklist

Use this checklist before releasing an app to real users. Adapt it to your application and skip items that genuinely don't apply.

Tick items off by changing `- [ ]` to `- [x]`. To have an AI coding assistant check the list against your real code, use [SKILL.md](SKILL.md).

This checklist is a starting point, not a guarantee of security or production readiness. Your app may need additional controls depending on its architecture, data sensitivity, scale, and business requirements.

## 1. High-Risk Checks

Start here. These issues can lead to unexpected costs, data loss, security incidents, or unauthorized access.

### Costs and Infrastructure

- [ ] Set spending limits and billing alerts for every paid API, especially AI model providers.
- [ ] Review usage limits and potential runaway costs.
- [ ] Back up the production database.
- [ ] Test restoring a backup, not just creating one.
- [ ] Document and test a rollback plan for failed deployments.

### Security and Secrets

- [ ] Check the current codebase and Git history for committed secrets.
- [ ] Rotate exposed credentials and revoke compromised keys.
- [ ] Store secrets securely outside source code.
- [ ] Apply rate limiting to public and sensitive endpoints.
- [ ] Verify authentication and authorization on every protected endpoint.
- [ ] Confirm that access controls are enforced on the server, not just in the UI.

## 2. Testing and Deployment

- [ ] Set up a CI/CD pipeline.
- [ ] Add unit tests for important application logic.
- [ ] Add smoke tests for critical user journeys.
- [ ] Add regression tests for previously fixed bugs and essential features.
- [ ] Create a staging environment separate from production.
- [ ] Audit dependencies for known vulnerabilities and outdated packages.
- [ ] Verify that production builds and deployment steps work as expected.

## 3. Monitoring and Observability

- [ ] Configure alerts for important errors and service failures.
- [ ] Add error tracking.
- [ ] Implement useful application logging.
- [ ] Monitor application performance and latency.
- [ ] Set up uptime monitoring.
- [ ] Add analytics appropriate to the product.
- [ ] Verify that alerts reach the right person and can be acted on.

## 4. Infrastructure and Performance

- [ ] Configure the custom domain and valid SSL/TLS certificates.
- [ ] Configure SPF, DKIM, and DMARC for your sending domain where applicable.
- [ ] Optimize image sizes and formats.
- [ ] Configure caching where appropriate.
- [ ] Review environment configuration for development, staging, and production.
- [ ] Confirm that critical services have suitable timeouts and failure handling.

## 5. AI-Specific Checks

*Only applicable if your application uses AI models or model-powered features.*

- [ ] Create repeatable evaluations (evals) for important model behaviors.
- [ ] Test for prompt injection and attempts to bypass instructions.
- [ ] Add a fallback or graceful failure path when a model API is unavailable or slow.
- [ ] Handle token limits, context overflow, and oversized inputs.
- [ ] Set model request timeouts and appropriate retry limits.
- [ ] Validate model outputs before using them in sensitive operations.
- [ ] Apply appropriate access controls to tools, data, and actions available to the model.
- [ ] Monitor model usage, latency, errors, and costs.

## 6. Users, Privacy, and Accessibility

- [ ] Test keyboard navigation and screen-reader compatibility.
- [ ] Check color contrast, labels, focus states, and accessible form errors.
- [ ] Publish an appropriate privacy policy and terms of service.
- [ ] Implement cookie consent where legally required.
- [ ] Provide a way for users to delete their accounts and associated data where applicable.
- [ ] Verify that password reset flows work, if passwords are supported.
- [ ] Verify email confirmation flows, if email verification is required.
- [ ] Check that sensitive user data is not unnecessarily exposed in logs or analytics.

## 7. User Experience and Launch Polish

- [ ] Implement a meaningful 404 page.
- [ ] Handle server errors with appropriate 500 responses or error screens.
- [ ] Include useful empty states.
- [ ] Include loading states and clear feedback during long-running actions.
- [ ] Add Open Graph (OG) images and a favicon.
- [ ] Validate SEO and AI search discoverability (AEO), including sitemap, `robots.txt`, and structured data where relevant.
- [ ] Test on multiple devices and screen sizes.
- [ ] Test on slow or unreliable networks.
- [ ] Document setup, configuration, architecture, testing, and deployment in a README.
- [ ] Verify the critical user journeys before launch.
