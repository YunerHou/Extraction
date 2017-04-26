# Extraction
#由于实例无法转换为OntClass列出子类，故只抽取出作为类的病因。然后将输出文件作为输入，解析出约束类（病因——诱发——疾病）

public class Extarct_bingyin {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		String filepath = "2.27.owl";
		OntModel base = ModelFactory.createOntologyModel(OntModelSpec.OWL_MEM);
		base.read(filepath);
		OntModel model = ModelFactory.createOntologyModel(OntModelSpec.OWL_MEM_MICRO_RULE_INF, base);

		System.out.println("本体模型读取成功");

				
		String SOURSE = "http://www.semanticweb.org/fan/ontologies/2016/7/untitled-ontology-26";
		String NS = SOURSE + "#";
    
		try {
			FileOutputStream out = new FileOutputStream("bingyin.ttl");
			OutputStreamWriter outWriter = new OutputStreamWriter(out, "UTF-8");
			BufferedWriter bw = new BufferedWriter(outWriter);
			
			 OntClass bingyin = model.getOntClass(NS+"心血管疾病病因");
			 ExtendedIterator<OntClass> i = bingyin.listSubClasses();
			 int s=0;
			 while(i.hasNext()){
				 s++;
				 OntClass reason = i.next();
				 System.out.println(reason.getLocalName());
					 bw.write(reason.getLocalName());
					 bw.newLine();
				 }
				 
				 
			 }
		 
				bw.close(); 
				outWriter.close(); 
				out.close();
			  
			 }catch (Exception e) { e.printStackTrace(); System.out.println("写入" +
			  "txt.ttl" + "出错！"); }
}
