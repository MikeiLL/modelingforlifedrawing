---
id: 45
title: 'Actual Income Calculator'
date: '2010-01-13T19:19:47+00:00'
layout: post
guid: 'http://modelingforlifedrawing.com/documents/?p=45'
permalink: /2010/01/13/actual-income-calculator/
categories:
    - Appendices
tags:
    - 'Actual Income Calculator'
---



You can prepare a financial cost-benefit analysis for each session:

<form id=calculator>
  <label>Hours Worked <input name=hrsworked type=number value=2></label>
  <label>Hourly Fee $<input name=hrlyfee type=number min="0.00" max="1000.00" step="0.10" value=20></label>
  <label>Expenses $<input name=expenses type=number min="0.00" max="1000.00" step="0.10" /></label>
  <label>Expense Reimbursement $<input name=reimbursement type=number min="0.00" max="1000.00" step="0.10" /></label>
  <label>Unpaid Time (In hours - include travel, other unpaid time) <input name=unpaidtime type=number /></label>
</form>

<div id=total>Fill in above fields to find calculated total.</div>

<script>
const hrsworked = document.querySelector('[name="hrsworked"]');
const hrlyfee = document.querySelector('[name="hrlyfee"]');
const expenses = document.querySelector('[name="expenses"]');
const reimbursement = document.querySelector('[name="reimbursement"]');
const unpaidtime = document.querySelector('[name="unpaidtime"]');
const total = document.getElementById("total");

[hrsworked,
hrlyfee,
reimbursement,
unpaidtime,
expenses].forEach((elem) => {
  elem.addEventListener("change", maybeCalculate);
});
let grossIncome = netIncome = 0;
function maybeCalculate(e) {
  grossIncome = +hrsworked.value * +hrlyfee.value;
  let result = "Gross Income " + new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(
    grossIncome,
  ) + ". ";
  netIncome = grossIncome;
  if (expenses.value) {netIncome -= +expenses.value; console.log("decrement expenses.value", netIncome); };
  if (reimbursement.value) {netIncome += +reimbursement.value; console.log("increment reimbursement.value", netIncome); };
  if (netIncome){
      result += "Net Income " + new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(
      netIncome,
    ) + ". ";
  }
  if (unpaidtime.value) {
    let totalTimeSpent = +unpaidtime.value + +hrsworked.value;
    result += "Overall hourly compensation " + new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(
    netIncome / totalTimeSpent
  ) + ". ";
  }
  total.textContent = result;
}
</script>


By adding together all income (fee and expense reimbursement) for that
session, subtracting costs not reimbursed from the total income, then
dividing by the total number of hours involved, including travel and
waiting time. Thus, if you are paid $30.00 for a three-hour session,
spend $5.00 for transportation, and take an hour each way, your total
time is five hours, your income is $30.00 – $5.00 = $25.00, divided by
5, = $5.00 per hour.

If this ratio seems lower than your time is worth, and there are no
reasons of friendship, education, professional advancement, curiosity,
and such that make you want to repeat work with people, discuss the
possibility of raising your fee or getting transportation
reimbursement. If this doesn’t work out, look for appointments
somewhere else.
