# Extraction
		try {
			FileOutputStream out = new FileOutputStream("bingyin.ttl");
			OutputStreamWriter outWriter = new OutputStreamWriter(out, "UTF-8");
			BufferedWriter bw = new BufferedWriter(outWriter);
			
			 StmtIterator state = model.listStatements();
			 while(state.hasNext()){
				 Statement bingyin = state.next();
				 String sub = bingyin.getSubject().getLocalName();
				 String pre = bingyin.getPredicate().getLocalName();
				 String obj = bingyin.getObject().toString();
				 if(obj.equals("http://www.semanticweb.org/fan/ontologies/2016/7/untitled-ontology-26#病因")){
					 System.out.println(sub+"   "+pre+"  "+obj);
					 String outline = "<http://dsc.nlp-bigdatalab.org:8086/"+sub+">          "
					 		+ "<http://www.w3.org/1999/02/22-rdf-syntax-ns#type>	      "
					 		+ "<http://dsc.nlp-bigdatalab.org:8086/"+obj+"> .";
					 bw.write(outline);
					 bw.newLine();
				 }
				 
				 
			 }
		 
				bw.close(); 
				outWriter.close(); 
				out.close();
			  
			 }catch (Exception e) { e.printStackTrace(); System.out.println("写入" +
			  "txt.ttl" + "出错！"); }
