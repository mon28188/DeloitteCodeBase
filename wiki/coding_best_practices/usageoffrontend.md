# Usage of frontend technologies

---

### Technologies used

Currently we are using 3 different technologies in our portals.

`Mijn PostNL` portal is using Visualforce, Lightning Aura and Lightning Web Components

`Mijn PostNL Zakelijk` portal is using only Lightning Web Components

As of `2020` we are working `only` with Lightning Web Components (LWC), and we just maintain the old functionalities in 
the other technologies.

### Visuaforce
Visualforce is a framework that allows developers to build custom user interfaces that can be hosted 
natively on the Lightning platform. The Visualforce framework includes a tag-based markup language, similar to HTML, 
and a set of server-side “standard controllers” that make basic database operations, such as queries and saves, 
very simple to perform.

### Aura
The Lightning Component framework is a UI framework for developing web apps for mobile and desktop devices. 
It’s a modern framework for building single-page applications with dynamic, responsive user interfaces 
for Lightning Platform apps. It uses JavaScript on the client-side and Apex on the server-side.

We have a library of base components used for implementations, you can find more information for it here: 
[Aura Base Components](/wiki/frontend/aurabase.md)

### LWC
Lightning Web Components uses core Web Components standards and provides only what’s necessary to perform well in 
browsers supported by Salesforce. Because it’s built on code that runs natively in browsers, Lightning Web Components 
is lightweight and delivers exceptional performance. Most of the code you write is standard JavaScript and HTML.

We have a library of base components used for implementations, you can find more information for it here:
[LWC Base Components](/wiki/frontend/lwcbase.md)

Because the `Mijn PostNL` portal is a Visualforce portal we had to use Aura apps as containers in order to implemnt
LWC's in this portal.

---

[Home](/wiki/Home.md) - [Coding best practices](/wiki/coding_best_practices/coding_best_practices.md) - Usage of frontend technologies
