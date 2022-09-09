<?php
defined('BASEPATH') or exit('No direct script access allowed');

class Product_m extends CI_Model
{

  public function get($id = null)
  {
    $this->db->select('tb_product.*, tb_distributor.name as distributor_name, tb_gudang.name as gudang_name, tb_kategori.name as kategori_name,
    tb_unit.name as unit_name');
    $this->db->join('tb_distributor', 'tb_product.distributor_id = tb_distributor.distributor_id');
    $this->db->join('tb_gudang', 'tb_product.gudang_id = tb_gudang.gudang_id');
    $this->db->join('tb_kategori', 'tb_product.kategori_id = tb_kategori.kategori_id');
    $this->db->join('tb_unit', 'tb_product.unit_id = tb_unit.unit_id');
    $this->db->from('tb_product');
    if ($id != null) {
      $this->db->where('product_id', $id);
    }
    $query = $this->db->get();
    return $query;
  }
  ?>
  
  
  //
  public function update_stock_in($data)
  {
    $qty = $data['qty'];
    $id = $data['product_id'];
    $sql = "UPDATE tb_product SET stock = stock + '$qty' WHERE product_id  = '$id' ";
    $this->db->query($sql);
  }
