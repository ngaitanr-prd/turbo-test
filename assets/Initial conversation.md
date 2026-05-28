**Alex:**

Hey, I’m Alex. I just got back from my honeymoon — I’m still a little jet-lagged and all over the place, so forgive me if I sound scattered. I’ve been trying to get this product out of Excel and into something more functional.

Right now, we manage all of our patient orders and billing flows inside a huge Excel spreadsheet. It’s basically an intake form for when a clinic sends us an order for a specific patient. But it’s become too complex to scale, and I’m looking for a more customizable, web-based tool where my team can input orders and generate the documents we need.

**Camila:**

Got it. So this is for your internal team — not something you’re building as a product for others?

**Alex:**

Exactly. It’s just for us. But even though it’s not customer-facing, I still want it to be clean, well-organized, and easy to use. If we’re going to invest in a system, I want something that actually makes our team’s day-to-day smoother. We’re a medical supply distributor that works with physical therapy clinics treating lymphedema and breast cancer patients. A therapist sends us an order for their patient. We collect all the documentation, do insurance verifications, submit prior authorizations if needed, place the order with the vendor, and manage billing. We drop ship everything to the patient and get paid by insurance.

**Camila:**

And the spreadsheet helps your team track and calculate all of that?

**Alex:**

Yeah — but it’s a beast. You enter the patient info, insurance, shipping address, and product details. Then we calculate our margin, cost per unit, billable amounts, and what the patient owes. Some of the logic depends on the vendor, product type, state, or payer. It pulls from three or four hidden tables — like fee schedules and product databases — to calculate everything. But it’s fragile. If one field breaks, the whole sheet goes haywire.

**Camila:**

What’s your goal for replacing it?

**Alex:**

I want a system that makes this process easier and less error-prone for our team. Ideally, we’d have two tables: one for products (with costs, vendors, and categories) and one for fee schedules (with payer rates and multipliers). Then, when an employee fills out the form, most fields would auto-populate. All they’d need to enter is the patient info and select the items from a dropdown.

The system should also generate three documents we rely on:

1. The encounter form — an internal document used to summarize the order.
2. The patient invoice — which we send out via DocuSign with a Stripe payment link.
3. The proof of delivery (POD) — which gets emailed to the patient after they receive their order, and must be signed.

**Camila:**

What’s the flow after an order is entered?

**Alex:**

First, the employee fills out the form. In some cases, certain HCPCS codes require a manager’s approval before proceeding — we currently manage that via SharePoint and a manual approval flow. After approval, we save the documents as PDFs, upload them to the patient’s record in our internal system, and send the invoice and consent via DocuSign.

If the patient pays, we go to the vendor portal and manually place the order. Then we send them the proof of delivery to sign.

**Camila:**

Would you want to automate sending those emails?

**Alex:**

That’s the dream. If the system could detect the vendor and send the order automatically to the right email — for example, if it’s a Medi product, send the order to Medi — that would save a lot of time. Right now, our team has to re-enter everything manually in the vendor portals, even though the info is already in the spreadsheet.

**Camila:**

Any other important features?

**Alex:**

Yes — two things:

- Some products require **measurement forms** from the therapist. We should be able to upload those per line item.
- Some patients are **self-pay**, so the price should default to the MSRP from the vendor catalog.

Also, I’d love to eventually track whether certain items require prior authorization. We know that internally, but it’s not written anywhere yet.