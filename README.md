// Parent Form data Fetch in Child table when we click on Fetch Value Button other data will be get flush
frappe.ui.form.on('Cloud Renewal', {
    refresh: function(frm) {
        frm.add_custom_button(__('Fetch Value'), function() {
            var parentValue = frm.doc.parent_input;
            var childTable = frm.fields_dict['sales_invoice_no'].grid;

            var row = frappe.model.add_child(cur_frm.doc, "Previous Plan Details", "plan_other_details");
            row.plan_opted = frm.doc.present_plan;
            row.plan_start_period = frm.doc.current_period_plan_date;
            row.plan_end_date = frm.doc.current_period_last_date;
            row.plan_paid = frm.doc.payment_status;
            row.sales_invoice_no = frm.doc.sales_invoice_no;
            row.sales_invoice_date = frm.doc.sales_invoice_date;
            row.sales_invoice_attachment = frm.doc.invoice_attachment;
            refresh_field("plan_other_details");

            // Code for Data Flush
            frm.refresh_fields();
            frm.set_value('plan_periodicity',"");
            frm.set_value('present_plan',"");
            frm.set_value('current_period_plan_date',"");
            frm.set_value('current_period_last_date',"");
            frm.set_value('payment_status',"");
            frm.set_value('sales_invoice_no',"");
            frm.set_value('sales_invoice_date',"");
            frm.set_value('invoice_attachment',"");
            
        });
            
    }
});
