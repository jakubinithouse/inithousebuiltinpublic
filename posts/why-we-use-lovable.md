# Why we use Lovable for everything (and where we don't)

*Posted 2026-05-26*

Every Inithouse product starts the same way: a Lovable project, a Supabase database, and a domain we bought for €10. That sameness isn't laziness — it's the whole strategy.

When you're running a portfolio of MVPs hunting for product-market fit, the cost of starting another experiment has to be near zero. Otherwise you only build the things that feel "safe enough to justify the time," which is exactly the wrong filter at the experimentation stage. Lovable collapses that cost. From idea to a live URL with auth, a database, payments, and a deployable React SPA: less than a day if you know what you're doing, less than a week if you're learning.

Three things matter beyond raw speed.

**Iteration cost stays low.** Once a product is shipped, the question is whether changes are cheap. Lovable lets us redo entire screens conversationally. That means we don't hesitate to throw out a layout we don't like — and "willingness to throw things out" is most of the work in finding PMF.

**The output is portable.** A Lovable project is just a React app on top of Supabase. Nothing locks us in. If a product hits traction and we need to eject — onboard a real engineer, refactor for scale, swap the auth — the code is right there. We've done it twice. Both times it took less than a week.

**It enforces a useful constraint.** Lovable is good at the 90% of UI work that's the same across every SaaS. It's clumsy at custom interactions, novel animations, anything that demands a designer's touch. That constraint pushes us toward products where the *idea* matters more than the *craft*. Which is the right tradeoff at MVP stage: the market doesn't care about your animation easing curves.

## Where Lovable isn't the right tool

We don't use Lovable for anything that needs precise pixel control, heavy state management across many views, or non-web interfaces. The two we run elsewhere both involve real-time interaction or unusual rendering pipelines — Lovable would still get you 70% there, but the last 30% would cost more than starting fresh in something else.

We also don't use it when the problem is "we have a working product and need to scale it past the prototype shape." At that point Lovable is the wrong tool: you want a real engineering codebase with tests, CI, and proper review. Lovable is the on-ramp, not the highway.

## The honest tradeoff

You give up some craft. You give up the satisfaction of writing the perfect component. You also give up about 90% of the time spent in the "yak shaving" zone of MVP development. For a portfolio of 17 products being run by a tiny team, that's not a tradeoff — it's the only viable path.

— Inithouse
