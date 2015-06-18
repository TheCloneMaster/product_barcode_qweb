# -*- coding: utf-8 -*-
##############################################################################
#
#    OpenERP, Open Source Management Solution
#    Copyright (C) 2004-2010 Tiny SPRL (<http://tiny.be>).
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as
#    published by the Free Software Foundation, either version 3 of the
#    License, or (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more summary.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <http://www.gnu.org/licenses/>.
#
##############################################################################

import time
from openerp.osv import osv, fields

import logging
_logger = logging.getLogger(__name__)

class product_barcode_print(osv.osv_memory):
    _name = 'product.barcode.print'
    _description = 'Product Barcode Print'

    _columns = {
        #'date_start': fields.date('Date Start', required=True),
        #'date_end': fields.date('Date End', required=True),
        'qty': fields.integer('Number of labels', help='How many labels to print'),
        'product_ids': fields.many2many('product.product', 'product_barcode_print_product_product_rel', 'product_id', 'wizard_id', 'Products to print labels'),
    }
    #_defaults = {
    #    'date_start': lambda *a: time.strftime('%Y-%m-%d'),
    #    'date_end': lambda *a: time.strftime('%Y-%m-%d'),
    #}

    def print_report(self, cr, uid, ids, context=None):
        """
         To get the parameters and print the report
         @param self: The object pointer.
         @param cr: A database cursor
         @param uid: ID of the user currently logged in
         @param context: A standard dictionary
         @return : retrun report
        """
        if context is None:
            context = {}
        datas = {'ids': context.get('active_ids', [])}
        res = self.read(cr, uid, ids, ['qty', 'product_ids'], context=context)
        res = res and res[0] or {}
        datas['form'] = res
        if res.get('id',False):
            datas['ids']=[res['id']]
        _logger.warning(datas)

        return self.pool['report'].get_action(cr, uid, [], 'product_barcode_qweb.report_product_barcode', data=datas, context=context)

# vim:expandtab:smartindent:tabstop=4:softtabstop=4:shiftwidth=4:
